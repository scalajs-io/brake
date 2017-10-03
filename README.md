Brake API for Scala.js
================================
[brake](https://www.npmjs.com/package/brake) - Throttle a stream with backpressure.

### Description

Throttle a stream with backpressure.

### Build Dependencies

* [SBT v0.13.16](http://www.scala-sbt.org/download.html)

### Build/publish the SDK locally

```bash
 $ sbt clean publish-local
```

### Running the tests

Before running the tests the first time, you must ensure the npm packages are installed:

```bash
$ npm install
```

Then you can run the tests:

```bash
$ sbt test
```

### Examples

```scala
import io.scalajs.nodejs.buffer.Buffer
import io.scalajs.nodejs.process
import io.scalajs.npm.brake.Brake
import io.scalajs.npm.readablestream.Readable

val bulk = new Readable()
bulk._read = () => {}

('A' to 'F') foreach { ch =>
  bulk.push(Buffer.from(String.valueOf(ch)))
}
bulk.push(null)
bulk.pipe(Brake(10)).pipe(process.stdout)
```

##### Output:

```text
ABCDEF
```

### Artifacts and Resolvers

To add the `Brake` binding to your project, add the following to your build.sbt:  

```sbt
libraryDependencies += "io.scalajs.npm" %%% "brake" % "0.4.1"
```

Optionally, you may add the Sonatype Repository resolver:

```sbt   
resolvers += Resolver.sonatypeRepo("releases") 