

page_type: reference


<!-- DO NOT EDIT! Automatically generated file. -->
# tfdbg.LocalCLIDebugWrapperSession

### `class tfdbg.LocalCLIDebugWrapperSession`



Defined in [`tensorflow/python/debug/wrappers/local_cli_wrapper.py`](https://www.github.com/tensorflow/tensorflow/blob/r1.1/tensorflow/python/debug/wrappers/local_cli_wrapper.py).

See the guide: [TensorFlow Debugger > Session wrapper class and `SessionRunHook` implementations](../../../api_guides/python/tfdbg#Session_wrapper_class_and_SessionRunHook_implementations)

Concrete subclass of BaseDebugWrapperSession implementing a local CLI.

This class has all the methods that a `session.Session` object has, in order
to support debugging with minimal code changes. Invoking its `run()` method
will launch the command-line interface (CLI) of tfdbg.

## Properties

<h3 id="graph"><code>graph</code></h3>



<h3 id="graph_def"><code>graph_def</code></h3>



<h3 id="sess_str"><code>sess_str</code></h3>



<h3 id="session"><code>session</code></h3>





## Methods

<h3 id="__init__"><code>__init__</code></h3>

``` python
__init__(
    sess,
    dump_root=None,
    log_usage=True,
    ui_type='curses'
)
```

Constructor of LocalCLIDebugWrapperSession.

#### Args:

* <b>`sess`</b>: The TensorFlow `Session` object being wrapped.
* <b>`dump_root`</b>: (`str`) optional path to the dump root directory. Must be a
    directory that does not exist or an empty directory. If the directory
    does not exist, it will be created by the debugger core during debug
    `run()` calls and removed afterwards.
* <b>`log_usage`</b>: (`bool`) whether the usage of this class is to be logged.
* <b>`ui_type`</b>: (`str`) requested UI type. Currently supported:
    (curses | readline)


#### Raises:

* <b>`ValueError`</b>: If dump_root is an existing and non-empty directory or if
    dump_root is a file.

<h3 id="__enter__"><code>__enter__</code></h3>

``` python
__enter__()
```



<h3 id="__exit__"><code>__exit__</code></h3>

``` python
__exit__(
    exec_type,
    exec_value,
    exec_tb
)
```



<h3 id="add_tensor_filter"><code>add_tensor_filter</code></h3>

``` python
add_tensor_filter(
    filter_name,
    tensor_filter
)
```

Add a tensor filter.

#### Args:

* <b>`filter_name`</b>: (`str`) name of the filter.
* <b>`tensor_filter`</b>: (`callable`) the filter callable. See the doc string of
    `DebugDumpDir.find()` for more details about its signature.

<h3 id="as_default"><code>as_default</code></h3>

``` python
as_default()
```



<h3 id="close"><code>close</code></h3>

``` python
close()
```



<h3 id="invoke_node_stepper"><code>invoke_node_stepper</code></h3>

``` python
invoke_node_stepper(
    node_stepper,
    restore_variable_values_on_exit=True
)
```

Overrides method in base class to implement interactive node stepper.

#### Args:

* <b>`node_stepper`</b>: (`stepper.NodeStepper`) The underlying NodeStepper API
    object.
* <b>`restore_variable_values_on_exit`</b>: (`bool`) Whether any variables whose
    values have been altered during this node-stepper invocation should be
    restored to their old values when this invocation ends.


#### Returns:

  The same return values as the `Session.run()` call on the same fetches as
    the NodeStepper.

<h3 id="on_run_end"><code>on_run_end</code></h3>

``` python
on_run_end(request)
```

Overrides on-run-end callback.

Actions taken:
  1) Load the debug dump.
  2) Bring up the Analyzer CLI.

#### Args:

* <b>`request`</b>: An instance of OnSessionInitRequest.


#### Returns:

  An instance of OnSessionInitResponse.

<h3 id="on_run_start"><code>on_run_start</code></h3>

``` python
on_run_start(request)
```

Overrides on-run-start callback.

Invoke the CLI to let user choose what action to take:
  `run` / `invoke_stepper`.

#### Args:

* <b>`request`</b>: An instance of `OnSessionInitRequest`.


#### Returns:

  An instance of `OnSessionInitResponse`.


#### Raises:

* <b>`RuntimeError`</b>: If user chooses to prematurely exit the debugger.

<h3 id="on_session_init"><code>on_session_init</code></h3>

``` python
on_session_init(request)
```

Overrides on-session-init callback.

#### Args:

* <b>`request`</b>: An instance of `OnSessionInitRequest`.


#### Returns:

  An instance of `OnSessionInitResponse`.

<h3 id="partial_run"><code>partial_run</code></h3>

``` python
partial_run(
    handle,
    fetches,
    feed_dict=None
)
```



<h3 id="partial_run_setup"><code>partial_run_setup</code></h3>

``` python
partial_run_setup(
    fetches,
    feeds=None
)
```

Sets up the feeds and fetches for partial runs in the session.

<h3 id="run"><code>run</code></h3>

``` python
run(
    fetches,
    feed_dict=None,
    options=None,
    run_metadata=None
)
```

Wrapper around Session.run() that inserts tensor watch options.

#### Args:

* <b>`fetches`</b>: Same as the `fetches` arg to regular `Session.run()`.
* <b>`feed_dict`</b>: Same as the `feed_dict` arg to regular `Session.run()`.
* <b>`options`</b>: Same as the `options` arg to regular `Session.run()`.
* <b>`run_metadata`</b>: Same as the `run_metadata` arg to regular `Session.run()`.


#### Returns:

  Simply forwards the output of the wrapped `Session.run()` call.


#### Raises:

* <b>`ValueError`</b>: On invalid `OnRunStartAction` value.


