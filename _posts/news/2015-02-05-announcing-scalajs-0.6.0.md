---
layout: post
title: Announcing Scala.js 0.6.0
category: news
tags: [releases]
---
{% include JB/setup %}

We are thrilled to announce the final release of Scala.js 0.6.0!

As of this version, we do not consider Scala.js to be experimental anymore.
We believe it has reached maturity, and from now on, the language semantics as well as the APIs will only evolve in backward compatible ways, or go through proper deprecation cycles.

Today is also the 2-year anniversary of Scala.js!
The [first commit](https://github.com/scala-js/scala-js/commit/9ad7627c2418e5d345375705ca087a60e3aa2c22) was pushed on February 5, 2013.

## Getting started

If you are new to Scala.js, head over to
[the tutorial]({{ BASE_PATH }}/doc/tutorial.html).

## Release notes

As the change in "major" version number witnesses, this release is *not* binary compatible with 0.5.x.
Libraries need to be recompiled and republished using 0.6.0 to be compatible.
More importantly, this release is not source compatible with 0.5.x either.

Please report any issues [on GitHub](https://github.com/scala-js/scala-js/issues).

The following libraries have already been upgraded and published for 0.6.0:

* [DOM types](https://github.com/scala-js/scala-js-dom): `"org.scala-js" %%% "scalajs-dom" % "0.7.0"`
* [jQuery types](https://github.com/scala-js/scala-js-jquery): `"be.doeraene" %%% "scalajs-jquery" % "0.7.0"`
* [Scala.rx](https://github.com/lihaoyi/scala.rx): `"com.lihaoyi" %%% "scalarx" % "0.2.7"`
* [µPickle](https://github.com/lihaoyi/upickle): `"com.lihaoyi" %%% "upickle" % "0.2.6"`
* [Autowire](https://github.com/lihaoyi/autowire): `"com.lihaoyi" %%% "autowire" % "0.2.4"`
* [scalajs-angulate](https://github.com/jokade/scalajs-angulate): `"biz.enef" %%% "scalajs-angulate" % "0.1"`
* [scalajs-angular](https://github.com/greencatsoft/scalajs-angular): `"com.greencatsoft" %%% "scalajs-angular" % "0.3"`
* [scalaz](https://github.com/japgolly/scalaz): `"com.github.inthenow" %%% "scalaz" % "7.1.0-4"` (via [@japgolly](https://github.com/japgolly))

The following testing frameworks are available:

* [µTest](https://github.com/lihaoyi/utest): `"com.lihaoyi" %%% "utest" % "0.3.0" % "test"`
* [MiniTest](https://github.com/monifu/minitest): `"org.monifu" %%% "minitest" % "0.11" % "test"`
* [Greenlight](https://github.com/greencatsoft/greenlight): `"com.greencatsoft" %%% "greenlight" % "0.1-SNAPSHOT" % "test"`
* [ScalaCheck](https://github.com/rickynils/scalacheck): `"com.github.inthenow" %%% "scalacheck" % "1.12.2" % "test"`
* [zCheck](https://github.com/InTheNow/zcheck): `"com.github.inthenow" %%% "zcheck" % "0.6.0" % "test"`

And the following helper sbt plugins as well:

* [Workbench](https://github.com/lihaoyi/workbench): `addSbtPlugin("com.lihaoyi" % "workbench" % "0.2.3")`
* @InTheNow's [sbt-scalajs](https://github.com/InTheNow/sbt-scalajs): `addSbtPlugin("com.github.inthenow" % "sbt-scalajs" % "0.6.0")`

There is also a new--and incompatible--version of the DOM API.
We recommend that you first upgrade to 0.7.0 and the above libraries while upgrading to Scala.js 0.6.0.
As a second step, you can upgrade to the DOM API version 0.8.0.
Libraries depending on the DOM API must also be republished against this version of the DOM API, since it is by and large incompatible with 0.7.0.
Here are the 0.8.0 versions of said libraries:

* [DOM types](https://github.com/scala-js/scala-js-dom): `"org.scala-js" %%% "scalajs-dom" % "0.8.0"`
* [jQuery types](https://github.com/scala-js/scala-js-jquery): `"be.doeraene" %%% "scalajs-jquery" % "0.8.0"`
* [ScalaTags](https://github.com/lihaoyi/scalatags): `"com.lihaoyi" %%% "scalatags" % "0.4.5"`
* [scalajs-angulate](https://github.com/jokade/scalajs-angulate) and [scalajs-angular](https://github.com/greencatsoft/scalajs-angular): not yet published

To start a Play! project with Scala.js, have a look at [play-with-scalajs-example](https://github.com/vmunier/play-with-scalajs-example).

## Preparations before upgrading from 0.5.x

### Upgrade to 0.5.6 if not already done

Before upgrading to 0.6.0, **we strongly recommend that you upgrade to Scala.js 0.5.6**, and address all deprecation warnings.
Scala.js 0.5.6 contains warnings for the most vicious breaking changes of 0.6.x.

### Migrate away from the Scala.js Jasmine test framework

If you use the Jasmine test framework wrapper for Scala.js (`scalajs-jasmine-test-framework`), migrate away from it to one of the other testing frameworks for Scala.js.
The Jasmine test framework wrapper is *not* a good testing framework for Scala.js code, and is being *removed* in 0.6.x.

Possible replacements:

* [uTest](https://github.com/lihaoyi/utest)
* [MiniTest](https://github.com/monifu/minitest)
* [Greenlight](https://github.com/greencatsoft/greenlight)
* [otest](https://github.com/cgta/otest)

Note that these testing frameworks also need to upgrade to 0.6.0 before you can use them.

## Upgrade to 0.6.0 from 0.5.6

Basically, you need to apply the same kind of changes to your build files as in [this commit](https://github.com/sjrd/scala-js-example-app/commit/6ccd5f64c3d46b203685a3c0762142513f5cc3e9), which mostly consists in:

* Upgrade to sbt >= 0.13.7.
* Adaptations to new groupId and artifact names for Scala.js packages.
* Adaptation to the new `AutoPlugin` infrastructure of the sbt plugin.
* Drop the prefix `ScalaJSKeys.` for Scala.js-specific sbt keys.
* Upgrade to 0.6.0-enabled versions of your dependencies.

On the sbt command line, not much changes, except the way you use the `fastOpt` and `fullOpt` stages.
In Scala 0.5.x, you could run in the `fastOpt` stage with:

    > fastOptStage::run

In 0.6.x, the stage is regulated by the setting `scalaJSStage`, which is one of:

* `PreLinkStage` (default): uses Rhino
* `FastOptStage`: `fastOpt` mode, uses Node.js or PhantomJS
* `FullOptStage`: `fullOpt` mode, uses Node.js or PhantomJS

You can change it from the command line with

    > set scalaJSStage := FastOptStage
    > run # runs in fastOpt mode

In a multi-project build, you'll want to change it for all projects, which can be done with `in Global`:

    > set scalaJSStage in Global := FastOptStage

## Major changes

This section discusses major changes affecting source compatibility, which may or may not apply to your project.

### `ClassCastException` becomes an undefined behavior

The JVM, in its incommensurable magnanimity, throws nicely specified exceptions when you do something bad with your code.
For example, it will nicely throw a `ClassCastException` if you perform an invalid `.asInstanceOf`, or an `ArithmeticException` if you divide an integer by 0.

Since the beginning of time, Scala.js has handled most of these things as *undefined behavior*, i.e., *anything can happen* if these cases happen.
Until 0.5.x, `ClassCastException`s were properly reported, though.
We have found, however, that checking these buggy cases costs up to 100% overhead to the overall execution time of a Scala.js program.

In Scala.js 0.6.x, therefore, invalid casts become an undefined behavior as well.
However, the compiler will *still* be nice with you *in the PreLink and FastOpt stages*, by throwing an `UndefinedBehaviorError` if you perform an invalid cast (instead of a `ClassCastException`).
`UndefinedBehaviorError` is a *fatal* error, meaning it won't be caught by `case NonFatal(e)` handlers.
In fullOpt mode, the checks are removed for maximum efficiency.

You *must not catch* `UndefinedBehaviorError`, since that would cause your program to behave differently in the fullOpt stage than in the other stages.
The idea of `UndefinedBehaviorError` is that you can enjoy strict checks and stack traces while developing.

If you really want `ClassCastException`s to be thrown reliably (in all stages), you can enable them in your application, at the expense of runtime performance, with the following sbt setting:

{% highlight scala %}
scalaJSSemantics ~= { _.withAsInstanceOfs(
    org.scalajs.core.tools.sem.CheckedBehavior.Compliant) }
{% endhighlight %}

This applies to the entire application, including dependencies.
There is no way to select parts of the application where this applies, because there is no way to make that sound.

### The `scala.scalajs.js` package has been simplified

We have removed a lot of historical warts from the `scala.scalajs.js` package, mostly types and APIs with equivalents among normal Scala types and libraries:

* `js.String`, `js.Boolean`, `js.Number` and `js.Undefined` have been removed, as well as their `js.prim.*` equivalent.
  `String`, `Boolean`, `Double` and `Unit` should be used instead, respectively.
* `js.parseInt(s)` and `js.parseFloat(s)` should be replaced by `s.toInt` and `s.toDouble`, respectively.
* `js.NaN`, `js.Infinity` should be replaced by `Double.NaN` and `Double.PositiveInfinity`, respectively.
* `js.isNaN(x)` should be replaced by `x.isNaN`.
* `js.isFinite(x)` should be replaced by `!x.isNaN && !x.isInfinite`.

Methods provided by ECMAScript 5.1 on primitive strings and numbers can be enabled by importing the following implicit conversions:

{% highlight scala %}
import js.JSStringOps._
import js.JSNumberOps._
{% endhighlight %}

### `js.native` in facade types

When writing facade types, it was previously recommended to use `???` as a fake body for fields and methods.
You should now use `js.native` instead, as in:

{% highlight scala %}
trait Foo extends js.Object {
  var bar: Int = js.native
  def foobar(x: Int): String = js.native
}
{% endhighlight %}

The compiler will emit a warning if you use any other body.
The warning will become an error in 1.0.0.

### `@JSExport` exports to fully qualified names by default

As announced by deprecation warnings in the 0.5.6 compiler, putting `@JSExport` without an explicit name on an `object` or `class` changes meaning between 0.5.x and 0.6.x.
Consider this code:

{% highlight scala %}
package babar

@JSExport
class Foo
{% endhighlight %}

In 0.5.x, `Foo` is exported as `Foo`.
In 0.6.x, it is exported as `babar.Foo` instead.

### Testing frameworks adaptations

If you are not a testing framework implementor, this section does not apply to you.
Please follow the migration guidelines of any testing framework you may use.

Until 0.5.x, Scala.js had a custom, ad-hoc substitute for the sbt testing interface, which allows testing frameworks to integrate with sbt.
Although quite good in its own right, it suffered from several limitations, including the inability for one project to use more than one testing framework at the same time, and severe discrepencies with the JVM sbt testing interface.
Scala.js 0.6.x now supports its JS version of the original sbt testing interface, with all its power, API, and usability features.
We also offer tools to make your testing framework fully source-compatible with the JVM and JS variants of the testing interface, without a single line of platform-specific source code.

An existing barebone cross-compiling testing framework can be found [in our tests](https://github.com/scala-js/scala-js/tree/v0.6.0/sbt-plugin-test).
Some highlights:

* [Build definition for the cross-compiling framework](https://github.com/scala-js/scala-js/blob/v0.6.0/sbt-plugin-test/build.sbt#L49-L64)
* [(Cross-compiling) source code of the testing framework](https://github.com/scala-js/scala-js/tree/v0.6.0/sbt-plugin-test/testFramework/src/main/scala/sbttest/framework)
* [Build definition for a cross-compiling project using the framework](https://github.com/scala-js/scala-js/blob/v0.6.0/sbt-plugin-test/build.sbt#L66-L86)
* [Source code of the project using the framework](https://github.com/scala-js/scala-js/tree/v0.6.0/sbt-plugin-test/multiTest)

Adapting your testing framework to follow this structure is likely to be the easiest path of migration.
You may also want to take a look at [the PR we made to uTest](https://github.com/lihaoyi/utest/pull/45) to migrate to Scala.js 0.6.x.

Should you run into trouble, don't hesitate to ask on the mailing list!

## Enhancements

### <a name="cross-project"></a> Defining cross-compiling projects with `crossProject`

When writing cross-compiling code, we need to have two separate projects in sbt for the JVM target and the JS target.
The new `CrossProject` type, and its `crossProject` builder, helps in defining these pairs of projects in a DRY way.

See the [documentation of `CrossProject`]({{ site.production_url }}/api/sbt-scalajs/0.6.0/#org.scalajs.sbtplugin.cross.CrossProject) for more information and examples.

### Faster!

Scala.js 0.6.0 benefits from many performance improvements, most notably:

* `asInstanceOf`s are unchecked (see above), giving `fullOpt` code up to twice as fast as before
* `Range.foreach`, aka the `for (i <- 0 until n)` kind of loops, is inlined away, giving the same performance as an explicit `while` loop.
* Higher-order operations on `js.Array`s and `js.Dictionary`s (such as `foreach`, `map`, etc.) are inlined away as `while` loops.
* Various improvements to the optimizer.

### Scala collection API for `js.Array[A]` and `js.Dictionary[A]`

The title says it all: `js.Array[A]` and `js.Dictionary[A]` receive the entire Scala collection API, respectively of `mutable.Buffer[A]` and `mutable.Map[String, A]`.

`js.Array` becomes the default implementation of `mutable.Buffer`, i.e., `mutable.Buffer.empty` returns a `js.Array` wrapped in a `js.WrappedArray`.

### Implicits to make "writing JavaScript" easier

Sometimes, for example when porting existing JavaScript code, we want to just "write JavaScript" inside our Scala.js code.
A new object `js.DynamicImplicits` ([API]({{ site.production_url }}/api/scalajs-library/0.6.0/#scala.scalajs.js.DynamicImplicits$)) provides implicit conversions that allow to write dynamically typed JavaScriptish code directly in Scala.js with a mimimal amount of boilerplate.
Needless to say, these implicits should be handled with care, but they can come in handy.

### On-demand strict floats

Scala.js under-specifies `Float` operations by default, saying that they can sometimes behave as if they were `Double`s.
In 0.6.x, you can configure your application to use *strict-float semantics*, guaranteeing that all `Float` operations behave as on the JVM, with the appropriate truncation of precision (with the notable exception of `.toString()`).
The following sbt setting enables this:

{% highlight scala %}
scalaJSSemantics ~= { _.withStrictFloats(true) }
{% endhighlight %}

Beware that this can have a major impact on performance on VMs that do not support the [`Math.fround`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/fround) function.

### Obfuscation of class names

The `scalaJSSemantics` option also allows to obfuscate or otherwise rename the class names in the emitted .js file, as was requested in [#1113](https://github.com/scala-js/scala-js/issues/1113).
For example, this sbt setting empties out all class names in the package `my.company`:

{% highlight scala %}
scalaJSSemantics ~= (_.withRuntimeClassName { linkedClass =>
  val fullName = linkedClass.fullName
  if (fullName.startsWith("my.company.")) ""
  else fullName
})
{% endhighlight %}

This changes the value returned by `x.getClass.getName` or `classOf[C].getName`.

### We publish to Maven Central

This should probably not affect sbt users, but it now becomes possible to imagine Maven and Gradle plugins for Scala.js.
To this effect, the sbt plugin codebase has also been refactored, and all parts that are not strictly bound to sbt as a build tool have been extracted in Mavenized artifacts.
An enthusiast Maven/Gradle user could therefore build a Maven/Gradle plugin with relatively few lines of code.
As a measurable figure, the code specific to sbt contains only 1,686 lines of code.

## Bugfixes

Amongst others, the following bugs have been fixed since 0.5.6:

* [#1430](https://github.com/scala-js/scala-js/issues/1430) `ClassTag.unapply` method (for deconstruction) fails for raw JS classes
* [#1423](https://github.com/scala-js/scala-js/issues/1423) String.getBytes returns trailing zeroes
* [#1324](https://github.com/scala-js/scala-js/issues/1324) Date.parse should return a Double, not an Int
* [#1349](https://github.com/scala-js/scala-js/issues/1349) Auto-completion in runMain task does not work
* [#1192](https://github.com/scala-js/scala-js/issues/1192) hashCode for floating points has a very bad distribution
* [#1402](https://github.com/scala-js/scala-js/issues/1402) `Traversers` does not handle the case of `Debugger`
* [#1451](https://github.com/scala-js/scala-js/issues/1451) ScalaDoc run crashes with property `@JSExports`
* [#1455](https://github.com/scala-js/scala-js/issues/1455) Runs for ScalaDoc complain about `@JSExport(SomeFinalVal)`
* [#1458](https://github.com/scala-js/scala-js/issues/1458) PhantomJS 2 expects a scheme name (`file:///`) for all urls, not just a path to local files
