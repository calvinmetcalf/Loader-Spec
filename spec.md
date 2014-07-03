

# <span class="secnum" id="sec-26.3">[26.3](#sec-loader-objects "link to this section")</span> Loader Objects

Loader objects are able to load the source code of an ECMAScript <span class="nt">Module</span> in the context of a      specific [Realm](#sec-code-realms).
    </div>    <section id="sec-reflect.loader-constructor">      <div class="front">

# <span class="secnum" id="sec-26.3.1">[26.3.1](#sec-reflect.loader-constructor "link to this section")</span> The Reflect.Loader Constructor

The initialize value of `Reflect.Loader` is the %Loader% intrinsic object. `Reflect.Loader` is        the constructor for Loader objects. When `Reflect.Loader` is called as a function rather than as a constructor,        it initializes its **this** value with the internal state necessary to support the        `Reflect.Loader.prototype` built-in methods.

The `Reflect.Loader` constructor is designed to be subclassable. It may be used as the value in an        `extends` clause of a class definition. Subclass constructors that intend to support the specified Loader        behaviour must include a `super` call to `Reflect.Loader`.
      </div>      <section id="sec-reflect.loader">

# <span class="secnum" id="sec-26.3.1.1">[26.3.1.1](#sec-reflect.loader "link to this section")</span>            Reflect.Loader ( [ options ] )

When the Reflect.Loader function is called with optional argument <var>options</var> the following steps are taken:

1.  Let _loader_ be the **this** value.
2.  If [Type](#sec-ecmascript-data-types-and-values)(_loader_) is not Object, throw a **TypeError**              exception.
3.  If _loader_ does not have a [[LoaderRecord]] [internal              slot](#sec-object-internal-methods-and-internal-slots), throw a **TypeError** exception.
4.  If the value of _loader_&rsquo;s [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots) is not **undefined**, throw a              **TypeError** exception.
5.  Let _realmObject_ be the result of [GetOption](#sec-getoption)(_options_,              `"realm"`).
6.  [ReturnIfAbrupt](#sec-returnifabrupt)(_realmObject_).
7.  If _realmObject_ is **undefined**, let _realm_ be the [Realm](#sec-code-realms) of [the running execution context](#sec-execution-contexts).
8.  Else,
    1.  If [Type](#sec-ecmascript-data-types-and-values)(_realmObject_) is not Object or                  _realmObject_ does not have a [[RealmRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots), throw a **TypeError**                  exception.
    2.  Let _realm_ be the value of  _realmObject_&rsquo;s [[RealmRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots).
    3.  If _realm_ is **undefined**,  throw a **TypeError** exception.9.  For each _name_ in the [List](#sec-list-and-record-specification-type) (`"normalize"`,              `"locate"`, `"fetch"`, `"translate"`, `"instantiate"`),
        1.  Let _hook_ be the result of [GetOption](#sec-getoption)(_options_, _name_).
    2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_hook_).
    3.  If _hook_ is not **undefined**,
        1.  If [IsCallable](#sec-iscallable)(_hook_) is **false,** throw a **TypeError**                      exception.
        2.  Let _result_ be [CreateDataPropertyOrThrow](#sec-createdatapropertyorthrow)(_loader_,                      _name_, _hook_).
        3.  [ReturnIfAbrupt](#sec-returnifabrupt)(_result_).10.  NOTE the following step ensures that this function was not reentrantly applied to <span style="font-family: Times              New Roman">_loader_</span> during the above steps.
11.  If the value of _loader_&rsquo;s [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots) is not **undefined**, throw a              **TypeError** exception.
12.  Let _loaderRecord_ be [CreateLoaderRecord](#sec-createloaderrecord)(_realm_,              _loader_).
13.  Set _loader_&rsquo;s [[LoaderRecord]] [internal              slot](#sec-object-internal-methods-and-internal-slots) to _loaderRecord_.
14.  Return _loader_.      </section>      <section id="sec-new-reflect.loader-argumentslist">

# <span class="secnum" id="sec-26.3.1.2">[26.3.1.2](#sec-new-reflect.loader-argumentslist "link to this section")</span> new Reflect.Loader ( ...argumentsList )

When `Reflect.Loader` is called as part of a `new` expression it is a constructor: it initializes        a newly created object. It  performs the following steps:

1.  Let _F_ be the `Reflect.Loader` function object on which the `new` operator was              applied.
2.  Let _argumentsList_ be the _argumentsList_ argument of the [[Construct]] internal method that was invoked              by the `new` operator.
3.  Return the result of [Construct](#sec-construct-f-argumentslist)(_F_, _argumentsList_).

If `Reflect.Loader` is implemented as an [ECMAScript function        object](#sec-ecmascript-function-objects), its [[Construct]] internal method will perform the above steps.
      </section>    </section>    <section id="sec-properties-of-the-loader-constructor">      <div class="front">

# <span class="secnum" id="sec-26.3.2">[26.3.2](#sec-properties-of-the-loader-constructor "link to this section")</span> Properties of the Loader Constructor

The value of the [[Prototype]] [internal slot](#sec-object-internal-methods-and-internal-slots) of the        `Reflect.Loader` constructor is the Function prototype object ([19.2.3](#sec-properties-of-the-function-prototype-object)).

Besides the `length` property (whose value is **0**), the `Reflect.Loader` constructor has the        following properties:
      </div>      <section id="sec-reflect.loader.prototype">

# <span class="secnum" id="sec-26.3.2.1">[26.3.2.1](#sec-reflect.loader.prototype "link to this section")</span> Reflect.Loader.prototype

The initial value of `Reflect.Loader.prototype` is the intrinsic %LoaderPrototype% object ([26.3.3](#sec-properties-of-the-reflect.loader-prototype-object)).

This property has the attributes { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]:        **false** }.
      </section>      <section id="sec-reflect.loader-@@create">

# <span class="secnum" id="sec-26.3.2.2">[26.3.2.2](#sec-reflect.loader-@@create "link to this section")</span> Reflect.Loader [ @@create ] ( )

The @@create method of a `Reflect.Loader` function object <var>F</var> performs the following steps:

1.  Let _F_ be the **this** value.
2.  Let _obj_ be the result of calling [OrdinaryCreateFromConstructor](#sec-ordinarycreatefromconstructor)(_F_,              `"%LoaderPrototype%"`, ([[LoaderRecord]])).
3.  Return _obj_.

The value of the `name` property of this function is `"[Symbol.create]"`.

This property has the attributes { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]:        **true** }.
      </section>    </section>    <section id="sec-properties-of-the-reflect.loader-prototype-object">      <div class="front">

# <span class="secnum" id="sec-26.3.3">[26.3.3](#sec-properties-of-the-reflect.loader-prototype-object "link to this section")</span> Properties of the Reflect.Loader Prototype Object

The value of the [[Prototype]] [internal slot](#sec-object-internal-methods-and-internal-slots) of the        `Reflect.Loader` prototype object is the standard built-in Object prototype object ([19.1.3](#sec-properties-of-the-object-prototype-object)). The `Reflect.Loader` prototype object is an        ordinary object. It does not have a [[LoaderRecord]] [internal        slot](#sec-object-internal-methods-and-internal-slots).

The phrase "<span style="font-family: Times New Roman">this Loader</span>" within the specification of the following        methods refers to the result returned by performing the abstract operation thisLoader with the **this** value of the        current method invocation passed as the argument.

The abstract operation thisLoader with argument <var>value</var> performs the following steps:

1.  If [Type](#sec-ecmascript-data-types-and-values)(_value_) is Object and _value_ has a              [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots), then
    1.  Let _r_ be _value_&rsquo;s [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots).
    2.  If _r_ is not **undefined**, then return _value_.2.  Throw a **TypeError** exception.      </div>      <section id="sec-reflect.loader.prototype.constructor">

# <span class="secnum" id="sec-26.3.3.1">[26.3.3.1](#sec-reflect.loader.prototype.constructor "link to this section")</span> Reflect.Loader.prototype.constructor

The initial value of `Reflect.Loader.prototype.constructor` is the built-in %Loader% constructor.
      </section>      <section id="sec-reflect.loader.prototype.define">

# <span class="secnum" id="sec-26.3.3.2">[26.3.3.2](#sec-reflect.loader.prototype.define "link to this section")</span> Reflect.Loader.prototype.define ( name, source [ , options ] )

The `define` method installs a module in this <var>loader</var>'s module registry for <var>source</var>        using <var>name</var> as the registry key. The module is not immediately available. The `translate` and        `instantiate` hooks are called asynchronously, and dependencies are loaded asynchronously. `define`        returns a Promise object that resolves to <span class="value">undefined</span> when the new module and its dependencies        are installed in the registry.

When the `define` method is called with arguments <var>name</var>, <var>source</var>, and optional argument        <var>options</var> the following steps are taken:

1.  Let _loader_ be this Loader.
2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_loader_).
3.  Let _loaderRecord_ be _loader&rsquo;s_ [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots).
4.  Let _name_ be [ToString](#sec-tostring)(_name_).
5.  [ReturnIfAbrupt](#sec-returnifabrupt)(_name_).
6.  Let _address_ be [GetOption](#sec-getoption)(_options_, `"address"`).
7.  [ReturnIfAbrupt](#sec-returnifabrupt)(_address_).
8.  Let _metadata_ be [GetOption](#sec-getoption)(_options_, `"metadata"`).
9.  [ReturnIfAbrupt](#sec-returnifabrupt)(_metadata_).
10.  If _metadata_ is **undefined** then let _metadata_ be [ObjectCreate](#sec-objectcreate)(%ObjectPrototype%).
11.  Let _p_ be [PromiseOfStartLoadPartwayThrough](#sec-promiseofstartloadpartwaythrough)(`"translate"`,              _loaderRecord_, _name_, _metadata_, _source_, _address_).
12.  [ReturnIfAbrupt](#sec-returnifabrupt)(_p_).
13.  Let _G_ be a new function as defined by ReturnUndefined.
14.  Let _p_ be the result of calling [PromiseThen](#sec-promisethen)(_p_, _G_).
15.  Return _p_.

The `length` property of the `define` method is **2**.
      </section>      <section id="sec-reflect.loader.prototype.delete">

# <span class="secnum" id="sec-26.3.3.3">[26.3.3.3](#sec-reflect.loader.prototype.delete "link to this section")</span> Reflect.Loader.prototype.delete ( name )

The `delete` method removes an entry whose key is <var>name</var> from this <var>loader</var>'s module        registry. It performs the following steps:

1.  Let _loader_ be this Loader.
2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_loader_).
3.  Let _loaderRecord_ be _loader&rsquo;s_ [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots).
4.  Let _name_ be [ToString](#sec-tostring)(_name_).
5.  [ReturnIfAbrupt](#sec-returnifabrupt)(_name_).
6.  Let _modules_ be the value of _loaderRecord_.[[Modules]],
7.  Repeat for each Record {[[_name_]], [[value]]} _p_ that is an element of _modules_,
      1.  If [SameValue](#sec-samevalue)(_p_.[[key]], _name_), then
        1.  Set _p_.[[key]] to <span style="font-family: sans-serif">empty</span>.
        2.  Set _p_.[[value]] to <span style="font-family: sans-serif">empty</span>.
        3.  Return **true**.8.  Return **false**.      </section>      <section id="sec-reflect.loader.prototype.entries">

# <span class="secnum" id="sec-26.3.3.4">[26.3.3.4](#sec-reflect.loader.prototype.entries "link to this section")</span> Reflect.Loader.prototype.entries ( )

The following steps are taken:

1.  Let _loader_ be this Loader.
2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_loader_).
3.  Return the result of [CreateLoaderIterator](#sec-createloaderiterator)(_loader_,              `"key+value"`).      </section>      <section id="sec-reflect.loader.prototype.get">

# <span class="secnum" id="sec-26.3.3.5">[26.3.3.5](#sec-reflect.loader.prototype.get "link to this section")</span> Reflect.Loader.prototype.get ( name )

If this Loader's module registry contains a Module with the given normalized <var>name</var>, return it. Otherwise,        return <span class="value">undefined</span>. If the module is in the registry but has never been evaluated, first        synchronously evaluate the bodies of the module and any dependencies that have not evaluated yet.

When the `get` method is called with the argument <var>name</var>, the following steps are taken:

1.  Let _loader_ be this Loader.
2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_loader_).
3.  Let _loaderRecord_ be _loader&rsquo;s_ [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots).
4.  Let _name_ be [ToString](#sec-tostring)(_name_).
5.  [ReturnIfAbrupt](#sec-returnifabrupt)(_name_).
6.  Let _modules_ be the value of _loaderRecord._[[Modules]],
7.  Repeat for each Record {[[key]], [[value]]} _p_ that is an element of _modules_,
      1.  If [SameValue](#sec-samevalue)(_p_.[[key]], _name_) is **true**, then
        1.  Let _module_ be _p_.[[value]].
        2.  Let _result_ be [EnsureEvaluated](#sec-ensureevaluated)(_module_,                      (),_loaderRecord_).
        3.  [ReturnIfAbrupt](#sec-returnifabrupt)(_result_).
        4.  Return _p_.[[value]].8.  Return **undefined**.      </section>      <section id="sec-get-reflect.loader.prototype.global">

# <span class="secnum" id="sec-26.3.3.6">[26.3.3.6](#sec-get-reflect.loader.prototype.global "link to this section")</span> get Reflect.Loader.prototype.global

`Reflect.Loader.prototype.global` is an accessor property whose set accessor function is <span        class="value">undefined</span>. Its get accessor function performs the following steps:

1.  Let _loader_ be this Loader.
2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_loader_).
3.  Let _loaderRecord_ be _loader&rsquo;s_ [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots).
4.  Let _realm_ be the value of _loaderRecord_.[[Realm]].
5.  Return _realm_.[[globalThis]].      </section>      <section id="sec-reflect.loader.prototype.has">

# <span class="secnum" id="sec-26.3.3.7">[26.3.3.7](#sec-reflect.loader.prototype.has "link to this section")</span> Reflect.Loader.prototype.has ( name )

When the `Reflect.Loader.prototype.**has**` method is called with argument <var>name</var> the following        steps are taken:

1.  Let _loader_ be this Loader.
2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_loader_).
3.  Let _loaderRecord_ be _loader&rsquo;s_ [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots).
4.  Let _name_ be [ToString](#sec-tostring)(_name_).
5.  [ReturnIfAbrupt](#sec-returnifabrupt)(_name_).
6.  Let _modules_ be the value of _loaderRecord._[[Modules]],
7.  Repeat for each Record {[[key]], [[value]]} _p_ that is an element of _modules_,
      1.  If [SameValue](#sec-samevalue)(_p_.[[key]], _name_) is **true**, then return                  **true**.
8.  Return **false**.

<span class="nh">NOTE</span> This method does not call any hooks or run any module code.

</section>      <section id="sec-reflect.loader.prototype.import">

# <span class="secnum" id="sec-26.3.3.8">[26.3.3.8](#sec-reflect.loader.prototype.import "link to this section")</span> Reflect.Loader.prototype.import ( name [ , options ] )

The `import` method asynchronously loads, links, and evaluates a module and all its dependencies if these        actions have not already been performed. The argument <var>name</var> is the registry key for the module.        `import` returns a Promise that resolves to the `Module` object once it has been committed to the        registry and evaluated.

When the `import` method is called with argument <var>name</var> and optional arguments <var>options</var>        the following steps are taken:

1.  Let _loader_ be this Loader.
2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_loader_).
3.  Let _loaderRecord_ be _loader&rsquo;s_ [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots).
4.  Let _p_ be the result of calling [LoadModule](#sec-loadmodule)(_loaderRecord_, _name_,              _options_).
5.  [ReturnIfAbrupt](#sec-returnifabrupt)(_p_).
6.  Let _F_ be a new function object as defined by EvaluateLoadedModule.
7.  Set _F_&rsquo;s [[Loader]] [internal slot](#sec-object-internal-methods-and-internal-slots) to              _loaderRecord_.
8.  Let _p_ be [PromiseThen](#sec-promisethen)(_p_, _F_).
9.  Return _p_.

If the optional argument <var>options</var> is an object with an `address` property the string value of that        property is used as the module location and module loading starts with the fetch step. If an `address` property        is not present,  module loading starts with the locate step.

The `length` property of the `import` method is **1**.
        <div class="note">

<span class="nh">NOTE</span> Invoking the `import` method is the dynamic equivalent (when combined with          normalization) of:
           <span class="prod"><span class="nt">ImportDeclaration</span> <span          class="geq">::</span> `import` <span class="nt">ModuleSpecifier</span> `;`</span>
        </div>      </section>      <section id="sec-reflect.loader.prototype.keys">

# <span class="secnum" id="sec-26.3.3.9">[26.3.3.9](#sec-reflect.loader.prototype.keys "link to this section")</span> Reflect.Loader.prototype.keys ( )

The following steps are taken:

1.  Let _loader_ be this Loader.
2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_loader_).
3.  Return the result of [CreateLoaderIterator](#sec-createloaderiterator)(_loader_,              `"key"`).      </section>      <section id="sec-reflect.loader.prototype.load">

# <span class="secnum" id="sec-26.3.3.10">[26.3.3.10](#sec-reflect.loader.prototype.load "link to this section")</span> Reflect.Loader.prototype.load ( name [ , options ] )

The `load` method asynchronously loads and links and all its dependencies if these actions have not already        been performed. The argument <var>name</var> is the registry key for the module. `load` returns a Promise that        resolves to the `Module` object once it has been committed to the registry.

When the `load` method is called with argument <var>name</var> and optional arguments <var>options</var> the        following steps are taken:

1.  Let _loader_ be this Loader.
2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_loader_).
3.  Let _loaderRecord_ be _loader&rsquo;s_ [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots).
4.  Let _p_ be the result of calling [LoadModule](#sec-loadmodule)(_loaderRecord_, _name_,              _options_).
5.  [ReturnIfAbrupt](#sec-returnifabrupt)(_p_).
6.  Let _p_ be [PromiseThen](#sec-promisethen)(_p_, %ReturnUndefined%).
7.  Return _p_.

If the optional argument <var>options</var> is an object with an `address` property. The string value of        that property is used as the module location and module loading starts with the fetch step. If an `address`        property is not present,  module loading starts with the locate step.

The `length` property of the `load` method is **1**.
        <div class="note">

<span class="nh">NOTE</span> The `load` method differs from the `import` method in that it does          not force evaluation of the loaded module.
        </div>      </section>      <section id="sec-reflect.loader.prototype.module">

# <span class="secnum" id="sec-26.3.3.11">[26.3.3.11](#sec-reflect.loader.prototype.module "link to this section")</span> Reflect.Loader.prototype.module ( source [, options ] )

The `module` method asynchronously loads, links, and evaluates an anonymous module from <var>source</var>.        The module's dependencies, if any, are loaded and committed to the registry. The anonymous module itself is not added to        the registry. `module` returns a Promise object that resolves to a new Module instance object once the given        module body has been evaluated.

When the `module` method is called with argument <var>source</var> and optional arguments <var>options</var>        the following steps are taken:

1.  Let _loader_ be this Loader.
2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_loader_).
3.  Let _loaderRecord_ be _loader&rsquo;s_ [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots).
4.  If _options_ was not passed, then let _options_ be **undefined**.
5.  Let _address_ be [GetOption](#sec-getoption)(_options_, `"address"`).
6.  [ReturnIfAbrupt](#sec-returnifabrupt)(_address_).
7.  Let _load_ be [CreateLoad](#sec-createload)(**undefined**).
8.  Set _load_.[[Address]] to _address_.
9.  Let _linkSet_ be [CreateLinkSet](#sec-createlinkset)(_loaderRecord_, _load_).
10.  Let _successCallback_ be a new function object as defined by EvaluateLoadedModule.
11.  Set _successCallback_&rsquo;s [[Loader]] [internal              slot](#sec-object-internal-methods-and-internal-slots) to _loaderRecord_.
12.  Set _successCallback_&rsquo;s [[Load]] [internal              slot](#sec-object-internal-methods-and-internal-slots) to _load_.
13.  Let _p_ be the result of calling [PromiseThen](#sec-promisethen)(_linkSet_.[[Done]],              _successCallback_).
14.  Let _sourcePromise_ be [PromiseOf](#sec-promiseof)(_source_).
15.  Perform [ProceedToTranslate](#sec-proceedtotranslate)(_loaderRecord_, _load_,              _sourcePromise_).
16.  Return _p_.

The optional argument <var>options</var> is an object with an `address` property.

The `length` property of the `module` method is **1**.
      </section>      <section id="sec-reflect.loader.prototype.newmodule">

# <span class="secnum" id="sec-26.3.3.12">[26.3.3.12](#sec-reflect.loader.prototype.newmodule "link to this section")</span> Reflect.Loader.prototype.newModule ( obj )

TO DO

In the prototype this is the Module Factory Function.  However, this factory seems to        have only specialized utility and it seems to unnecessarily clutter the &ldquo;global&rdquo; namespace of Module        abstractions.  Making it a method of module loaders seems like a more sanity thing to do, but we can break it out if        that;s what people really want.

Also need to reconcile with are execute factory returns by the instantiate hook.  Is        this method intended to be able as an execute factory.  If sho it probably needs to accept multiple arguments.

When the `newModule` method is called with argument <var>obj</var> it creates a new Module objects whose        export properties are derived form the properties of <var>obj</var>. The following steps are performed:

1.  If [Type](#sec-ecmascript-data-types-and-values)(_obj_) is not Object, throw a **TypeError**              exception.
2.  Let _mod_ be CreateLinkedModuleInstance( )
3.  Let _keys_ be the result of calling the ObjectKeys abstract operation passing _obj_ as the argument.
4.  [ReturnIfAbrupt](#sec-returnifabrupt)(_keys_).
5.  For each _key_ in _keys_, do
    1.  Let _value_ be the result of [Get](#sec-get-o-p)(_obj_, _key_).
    2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_value_).
    3.  Let _F_ be the result of calling CreateConstantGetter(_key_, _value_).
    4.  Let _desc_ be the PropertyDescriptor {[[Configurable]]: **false**, [[Enumerable]]: **true**, [[Get]]:                  _F_, [[Set]]: **undefined**}.
    5.  Let _status_ be the result of calling the [DefinePropertyOrThrow](#sec-definepropertyorthrow)                  abstract operation passing _mod_, _key_, and _desc_ as arguments.
    6.  [ReturnIfAbrupt](#sec-returnifabrupt)(_status_).6.  Call the [[PreventExtensions]] internal method of _mod_.
7.  Return _mod_.      </section>      <section id="sec-get-reflect.loader.prototype.realm">

# <span class="secnum" id="sec-26.3.3.13">[26.3.3.13](#sec-get-reflect.loader.prototype.realm "link to this section")</span> get Reflect.Loader.prototype.realm

`Reflect.Loader.prototype.realm` is an accessor property whose set accessor function is <span        class="value">undefined</span>. Its get accessor function performs the following steps:

1.  Let _loader_ be this Loader.
2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_loader_).
3.  Let _loaderRecord_ be _loader&rsquo;s_ [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots).
4.  Return RealmObjectFor(_loaderRecord_.[[Realm]]).      </section>      <section id="sec-reflect.loader.prototype.set">

# <span class="secnum" id="sec-26.3.3.14">[26.3.3.14](#sec-reflect.loader.prototype.set "link to this section")</span> Reflect.Loader.prototype.set ( name, module )

Store a <span style="font-family: Times New Roman">Module obj</span> in this Loader's <var>module</var> registry,        overwriting any existing entry with the same <var>name</var>.

The following steps are taken:

1.  Let _loader_ be this Loader.
2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_loader_).
3.  Let _loaderRecord_ be _loader&rsquo;s_ [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots).
4.  Let _name_ be [ToString](#sec-tostring)(_name_).
5.  [ReturnIfAbrupt](#sec-returnifabrupt)(_name_).
6.  If [Type](#sec-ecmascript-data-types-and-values)(_module_) is not Object, throw a **TypeError**              exception.
7.  Let _modules_ be the value of _loaderRecord._[[Modules]],
8.  Repeat for each Record {[[key]], [[value]]} _p_ that is an element of _modules_,
      1.  If [SameValue](#sec-samevalue)(_p_.[[key]], _name_) is **true**, then
        1.  Set _p_.[[value]] to _module_.
        2.  Return _loader_.9.  Let _p_ be the Record {[[key]]: _name_, [[value]]: _module_}.
10.  Append _p_ as the last record of _loaderRecord_.[[Modules]].
11.  Return _loader_.      </section>      <section id="sec-reflect.loader.prototype.values">

# <span class="secnum" id="sec-26.3.3.15">[26.3.3.15](#sec-reflect.loader.prototype.values "link to this section")</span> Reflect.Loader.prototype.values ( )

The following steps are taken:

1.  Let _loader_ be this Loader.
2.  [ReturnIfAbrupt](#sec-returnifabrupt)(_loader_).
3.  Return the result of [CreateLoaderIterator](#sec-createloaderiterator)(_loader_,              `"value"`).      </section>      <section id="sec-reflect.loader.prototype-@@iterator">

# <span class="secnum" id="sec-26.3.3.16">[26.3.3.16](#sec-reflect.loader.prototype-@@iterator "link to this section")</span> Reflect.Loader.prototype[@@iterator] ( )

The initial value of the @@iterator property is the same function object as the initial value of the        `entries` property.
      </section>      <section id="sec-reflect.loader.prototype-@@tostringtag">

# <span class="secnum" id="sec-26.3.3.17">[26.3.3.17](#sec-reflect.loader.prototype-@@tostringtag "link to this section")</span> Reflect.Loader.prototype [ @@toStringTag ]

The initial value of the @@toStringTag property is the string value `"Reflect.Loader"`.

This property has the attributes { [[Writable]]: <span class="value">false</span>, [[Enumerable]]: <span        class="value">false</span>, [[Configurable]]: <span class="value">true</span> }.
      </section>      <section id="sec-reflect.loader-pipeline-hook-properties">        <div class="front">

# <span class="secnum" id="sec-26.3.3.18">[26.3.3.18](#sec-reflect.loader-pipeline-hook-properties "link to this section")</span> Reflect.Loader Pipeline Hook Properties

Loader hooks are methods that are called at various points in the process of loading a module.          `Loader.prototype` provides default implementations for the hook methods. However, individual Loader object          may over-ride these defaults using own properties.
        </div>        <section id="sec-reflect.loader.prototype.normalize">

# <span class="secnum" id="sec-26.3.3.18.1">[26.3.3.18.1](#sec-reflect.loader.prototype.normalize "link to this section")</span> Reflect.Loader.prototype.normalize ( name, refererName,              refererAddress )

When the `normalize` loader hook is called with arguments  <var>name</var>, <var>refererName</var>, and          <var>refererAddress</var> <var>loadRequest</var>, the following steps are taken:

1.  [Assert](#sec-algorithm-conventions): [Type](#sec-ecmascript-data-types-and-values)(_name_) is String.
2.  Return _name_.

This is a Loader hook that may be over-ridden by an own property of Loader instances. The `normalize` hook          is called once per distinct <span class="nt">ModuleSpecifier</span> String value in a <span          class="nt">ModuleBody</span>, while the module <span class="nt">ModuleBody</span> with that  is being loaded. The          <var>name</var> argument is the StringValue of a <span class="nt">ModuleSpecifier</span>.

The `normalize` hook returns an eventual String, the normalized module name, which is used for the rest of          the import process. In particular, the [[Loads]] and [[Modules]] Lists of a ModuleLinkage record are both keyed by          normalized module names. The module registry contains at most one module for a given normalized module name.

After calling this hook, if the normalized module <var>name</var> is in the registry or the load table, no new Load          Record is created. Otherwise the loader initiates a load for that module that starts by calling the `locate`          hook.
        </section>        <section id="sec-reflect.loader.prototype.locate">

# <span class="secnum" id="sec-26.3.3.18.2">[26.3.3.18.2](#sec-reflect.loader.prototype.locate "link to this section")</span> Reflect.Loader.prototype.locate ( loadRequest )

When the locate method is called with argument <var>loadRequest</var> the following steps are taken:

1.  Return the result of [Get](#sec-get-o-p)(_loadRequest_, `"name"`).

This is a Loader hook that may be over-ridden by an own property of Loader instances. The `locate` hook is          called for each distinct normalized import <span class="nt">ModuleSpecifier</span> immediately after the          `normalize` hook returns successfully, unless the module is already loaded or loading.

The `locate` hook is called to obtain to determine the Loader-dependent resource address (URL, path, etc.)          corresponding to normalized module name. The resource address is used later in the Loader pipeline to retrieve the          source code of the requested module.

When a `locate` hook is called by an Loader object the argument <var>loadRequest</var> is a LoadRequest          object ([15.2.3.2](#sec-load-records-and-loadrequest-objects)). The value of the `name` property          is the normalized module name. The `locate` hook returns an eventual value that is used as the resource          address. When the returned value is resolved, loading will continue with the `fetch` hook.
          <div class="note">

<span class="nh">NOTE</span> The `System.locate` hook typically is significantly more complicated than            the default `locate` hook.
          </div>        </section>        <section id="sec-reflect.loader.prototype.fetch">

# <span class="secnum" id="sec-26.3.3.18.3">[26.3.3.18.3](#sec-reflect.loader.prototype.fetch "link to this section")</span> Reflect.Loader.prototype.fetch ( loadRequest )

When the `fetch` loader hook is called with argument <var>loadRequest</var>, the following steps are          taken:

1.  Throw a **TypeError** exception.

This is a Loader hook that will normally be over-ridden by an own property of Loader instances. The          `fetch` hook is called by a Loader for all modules whose source code was not directly provided to the Loader.          It is also used to process the `import` keyword. The `fetch` hook is not called for module bodies          directly provided as arguments to `loader.module()` or `loader.define()`. However, the          `fetch` hook may be called when loading other modules imported by such modules.

When a `fetch` hook is called by an Loader object the argument <var>loadRequest</var> is a LoadRequest          object ([15.2.3.2](#sec-load-records-and-loadrequest-objects)) with an `address` property. The          value of the `address` property identifies the module source code to fetch.  The fetch hook returns an          eventual String containing the source  code of the module.
        </section>        <section id="sec-reflect.loader.prototype.translate">

# <span class="secnum" id="sec-26.3.3.18.4">[26.3.3.18.4](#sec-reflect.loader.prototype.translate "link to this section")</span> Reflect.Loader.prototype.translate ( loadRequest )

When the translate method is called, the following steps are taken:

1.  Return the result of [Get](#sec-get-o-p)(_loadRequest_, `"source"`).

This is a `Loader` hook that may be over-ridden by an own property of Loader instances. The          `translate` hook is called for each <span class="nt">ModuleBody</span> including those passed to          `loader.module()` or `loader.define()`.The `translate` hook is called prior to parsing          the <span class="nt">ModuleBody</span> and provides a Loader the opportunity to modify or replace the source code that          will be parsed.
          <div class="note">

<span class="nh">NOTE</span> An example of the use of the `translate` hook would be to translate source            code for a another programing language into an ECMAScript _ModuleBody_.
          </div>

When a `translate` hook is called by an Loader object the argument <var>loadRequest</var> is a LoadRequest          object ([15.2.3.2](#sec-load-records-and-loadrequest-objects)) with `address` and          `source` properties. The value of the `address` property identifies the module source code to          fetch. The value of the `source` property is the resolved value returned from the `fetch` hook.          The `translate` hook returns either an eventual String value ECMAScript that will be parsed as a <span          class="nt">ModuleBody</span>.
        </section>        <section id="sec-reflect.loader.prototype.instantiate">

# <span class="secnum" id="sec-26.3.3.18.5">[26.3.3.18.5](#sec-reflect.loader.prototype.instantiate "link to this section")</span> Reflect.Loader.prototype.instantiate ( loadRequest )

When the instantiate loader hook is called with argument <var>loadRequest</var>, the following steps are taken:

1.  Return **undefined**.

This hook allows a Loader to provide interoperability with other module systems.

When a `instantiate` hook is called by an Loader object the argument, <var>loadRequest</var>, is a          LoadRequest object ([15.2.3.2](#sec-load-records-and-loadrequest-objects)) with `address` and          `source` properties.  <var>loadRequest</var>`.name`, <var>loadRequest</var>`.metadata`,          and <var>loadRequest</var>`.address` are the same values passed to the `fetch` and          `translate` hooks. <var>loadRequest</var>`.source` is the value produced by the          `translate` hook.

If the `instantiate` hook returns an eventual **undefined**, then the loader uses the default linking          behaviour. It parses <var>loadRequest</var>`.source` as a Module, looks at its imports, loads its          dependencies asynchronously, and finally links them together and adds them to the registry.

Otherwise, the `instantiate` hook must return an eventual <var>instantiationRequest</var> object. An          <var>instantiateRequest</var> object has two required properties. The value of the `deps` property is an          array of strings. Each string is the name of a module upon which the module identified by <var>loadRequest</var> has          dependencies. The value of the `execute` property is a function which the loader will use to create the          module and link it with its clients and dependencies. The function should expect to receive the same number of arguments          as the size of the `deps` array and must return an eventual  Module object.  The arguments are Module objects          and have a one-to-one correspondence with elements of the `deps` array.

The module is evaluated during the linking process. First all of the modules it depends upon are linked and evaluated          , and then passed to the `execute` function. Then the resulting module is linked with the downstream          dependencies.
          <div class="note">

<span class="nh">NOTE</span> This feature is provided in order to permit custom loaders to support using            `import` to import pre-ES6 modules such as AMD modules. The design requires incremental linking when such            modules are present, but it ensures that modules implemented with standard source-level module declarations can still            be statically validated.
          </div>        </section>      </section>    </section>    <section id="sec-properties-of-reflect.loader-instances">

# <span class="secnum" id="sec-26.3.4">[26.3.4](#sec-properties-of-reflect.loader-instances "link to this section")</span> Properties of Reflect.Loader Instances

Loader instances are ordinary objects that inherit properties from the %LoaderPrototype% intrinsic  object. Loader      instances each have a [[Loader]] interal slot whose value after initialization is the Loader Record that the Load instance      reflects.
    </section>    <section id="sec-loader-iterator-objects">      <div class="front">

# <span class="secnum" id="sec-26.3.5">[26.3.5](#sec-loader-iterator-objects "link to this section")</span> Loader Iterator Objects

A Loader Iterator object represents a specific iteration over the module registry of some specific Loader instance        object. There is not a named constructor for Loader Iterator objects.  Instead, Loader iterator objects are created by        calling certain methods of Loader instance objects.
      </div>      <section id="sec-createloaderiterator">

# <span class="secnum" id="sec-26.3.5.1">[26.3.5.1](#sec-createloaderiterator "link to this section")</span> CreateLoaderIterator Abstract Operation

Several methods of Loader objects return Iterator objects. The abstract operation CreateLoaderIterator with arguments        <var>loader</var> and <var>kind</var> is used to create such iterator objects. It performs the following steps:

1.  [Assert](#sec-algorithm-conventions): _loader_ is an initialized Loader instance object.
2.  Let _iterator_ be [ObjectCreate](#sec-objectcreate)(<span style="font-family:              sans-serif">%LoaderIteratorPrototype%</span>,  ([[Loader]], [[LoaderNextIndex]], [[LoaderIterationKind]])).
3.  Set _iterator&rsquo;s_ [[Loader]] [internal slot](#sec-object-internal-methods-and-internal-slots)              to _loader_.
4.  Set _iterator&rsquo;s_ [[LoaderNextIndex]] [internal              slot](#sec-object-internal-methods-and-internal-slots) to 0.
5.  Set _iterator&rsquo;s_ [[LoaderIterationKind]] [internal slot](#sec-object-internal-methods-and-internal-slots) to _kind_.
6.  Return _iterator_.      </section>      <section id="sec-%loaderiteratorprototype%-object">        <div class="front">

# <span class="secnum" id="sec-26.3.5.2">[26.3.5.2](#sec-%loaderiteratorprototype%-object "link to this section")</span> The %LoaderIteratorPrototype% Object

All Loader Iterator Objects inherit properties from the %LoaderIteratorPrototype% intrinsic object.  The          %LoaderIteratorPrototype% intrinsic object is an ordinary object and its [[Prototype]] [internal slot](#sec-object-internal-methods-and-internal-slots) is the %ObjectPrototype% intrinsic object. In          addition, %LoaderIteratorPrototype% has the following properties:
        </div>        <section id="sec-%loaderiteratorprototype%.next">

# <span class="secnum" id="sec-26.3.5.2.1">[26.3.5.2.1](#sec-%loaderiteratorprototype%.next "link to this section")</span> %LoaderIteratorPrototype%.next ( )

1.  Let _O_ be the **this** value.
2.  If [Type](#sec-ecmascript-data-types-and-values)(_O_) is not Object, throw a **TypeError**                exception.
3.  If _O_ does not have all of the internal slots of a Loader Iterator Instance ([26.3.5.3](#sec-properties-of-loader-iterator-instances)), throw a **TypeError** exception.
4.  Let _m_ be the value of the [[Loader]] [internal                slot](#sec-object-internal-methods-and-internal-slots) of _O_.
5.  Let _loaderRecord_ be _m&rsquo;s_ [[LoaderRecord]] [internal slot](#sec-object-internal-methods-and-internal-slots).
6.  Let _index_ be the value of the [[LoaderNextIndex]] [internal slot](#sec-object-internal-methods-and-internal-slots) of _O_.
7.  Let _itemKind_ be the value of the [[LoaderIterationKind]] [internal slot](#sec-object-internal-methods-and-internal-slots) of _O_.
8.  If _m_ is **undefined**, then return [CreateIterResultObject](#sec-createiterresultobject)(**undefined**, **true**).
9.  Let _entries_ be the [List](#sec-list-and-record-specification-type) that is the value of the                _loaderRecord_.[[Modules]].
10.  Repeat while _index_ is less than the total number of elements of _entries_. The number of elements must                be redetermined each time this method is evaluated.
        1.  Let _e_ be the Record {[[key]], [[value]]} that is the value of _entries_[_index_].
    2.  Set _index_ to _index_+1;
    3.  Set the [[LoaderNextIndex]] [internal slot](#sec-object-internal-methods-and-internal-slots) of                    _O_ to _index_.
    4.  If _e_.[[key]] is not <span style="font-family: sans-serif">empty</span>, then
        1.  If _itemKind_ is **"`key`"** then, let _result_ be _e_.[[key]].
        2.  Else if _itemKind_ is **"`value`"** then, let _result_ be _e_.[[value]].
        3.  Else,
            1.  [Assert](#sec-algorithm-conventions): _itemKind_ is `"key+value"`.
            2.  Let _result_ be the result of performing [ArrayCreate](#sec-arraycreate)(2).
            3.  [Assert](#sec-algorithm-conventions): _result_ is a new, well-formed Array object so                            the following operations will never fail.
            4.  Call [CreateDataProperty](#sec-createdataproperty)(_result_, **"`0`"**,                            _e_.[[key]]) .
            5.  Call [CreateDataProperty](#sec-createdataproperty)(_result_, **"`1`"**,                            _e_.[[value]]).4.  Return [CreateIterResultObject](#sec-createiterresultobject)(_result_, **false**).11.  Set the [[Loader]] [internal slot](#sec-object-internal-methods-and-internal-slots) of _O_ to                **undefined**.
12.  Return [CreateIterResultObject](#sec-createiterresultobject)(**undefined**, **true**).          <div class="note">

<span class="nh">NOTE</span> Setting  the [[Loader]] [internal slot](#sec-object-internal-methods-and-internal-slots) to undefined when the iterator is exhausted            ensures that the same iterator cannot be restarted if new entries are subsequently added. This condition is tested in            step 8.
          </div>        </section>        <section id="sec-%loaderiteratorprototype%-@@iterator">

# <span class="secnum" id="sec-26.3.5.2.2">[26.3.5.2.2](#sec-%loaderiteratorprototype%-@@iterator "link to this section")</span> %LoaderIteratorPrototype% [ @@iterator ] ( )

The following steps are taken:

1.  Return the **this** value.

The value of the `name` property of this function is `"[Symbol.iterator]"`.
        </section>        <section id="sec-%loaderiteratorprototype%-@@tostringtag">

# <span class="secnum" id="sec-26.3.5.2.3">[26.3.5.2.3](#sec-%loaderiteratorprototype%-@@tostringtag "link to this section")</span> %LoaderIteratorPrototype% [ @@toStringTag ]

The initial value of the @@toStringTag property is the string value **"`Loader Iterator`"**.
        </section>      </section>      <section id="sec-properties-of-loader-iterator-instances">

# <span class="secnum" id="sec-26.3.5.3">[26.3.5.3](#sec-properties-of-loader-iterator-instances "link to this section")</span> Properties of Loader Iterator Instances

Loader Iterator instances are ordinary objects that inherit properties from the %LoaderIteratorPrototype% intrinsic        object. Loader Iterator instances are initially created with the internal slots described in [Table        51](#table-51).
        <figure>          <figcaption><span id="table-51">Table 51</span> &mdash; Internal Slots of Loader Iterator Instances</figcaption>          <table class="real-table">            <tr>              <th style="border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-top: 2px solid #000000">Internal Slot</th>              <th style="border-bottom: 1px solid #000000; border-left: 0px solid black; border-right: 1px solid #000000; border-top: 2px solid #000000">Description</th>            </tr>            <tr>              <td>[[Loader]]</td>              <td>The Loader object that is being iterated.</td>            </tr>            <tr>              <td>[[LoaderNextIndex]]</td>              <td>The integer index of the next Loader registry data element to be examined by this iterator.</td>            </tr>            <tr>              <td>[[LoaderIterationKind]]</td>              <td>A string value that identifies what is to be returned for each element of the iteration. The possible values are: **"`key`"**, **"`value`"**, **"`key+value`"**.</td>            </tr>          </table>        </figure>      </section>    </section>  </section>  <section id="sec-system-object">
