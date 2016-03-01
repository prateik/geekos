# Error Handling in GeekOS #

All GeekOS functions that can fail should return an
int value: 0 if the function call was successful,
or an error code selected from <geekos/errno.h>
if unsuccessful.

Functions that need to "return" a value, such as a pointer
to a created data structure, should do so by assigning to a
pointer parameter.

## Cleanup Functions ##

All objects requiring some kind of end-of-life
cleanup (freeing memory, closing devices, etc.)
should have a robust cleanup function.  The cleanup
function should handle a null pointer by simply
returning.  Otherwise, the cleanup function does what
it needs to do to tear down the object.

## Cleanup Code ##

One of the most important issues in writing functions
that allocate multiple resources is figuring out how to
"back out" if a failure occurs, making sure that
any partially-complete resource creation has been
cleaned up.

As long as all cleanup functions can correctly handle
a null pointer as an argument, the following
general idiom works well:

```
  struct foo *res1 = 0;
  struct bar *res2 = 0;
  struct baz *res3 = 0;
  struct thud *obj;   /* the object we want to create */
  int rc;

  if ((rc = foo_create(..., &res1)) != 0) {
	goto fail;
  }

...

  if ((rc = bar_create(..., &res2)) != 0) {
	goto fail;
  }

...

  if ((rc = baz_create(..., &res3)) != 0) {
	goto fail;
  }

  /* all required resources created successfully */
  obj = thud_create(res1, res2, res3);
  *p_obj = obj; /* assuming that p_obj is a parameter whose type is struct thud ** */
  return 0;

fail:
  /* de-allocate resources in reverse order */
  baz_destroy(res3);
  bar_destroy(res2);
  foo_destroy(res1);
  return rc;
```