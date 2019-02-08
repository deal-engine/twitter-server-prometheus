# Twitter Server Prometheus Exporter

This project is a simple metrics exporter from twitter server to prometheus based on the blog post and code from [Footballradar](https://engineering.footballradar.com/prometheus-at-football-radar/)

## Features

* Metrics are exposed on the admin port `/metrics` http endpoint.
* The service is detached from the main thread pool of the rest of the app just like the `/admin/metrics.json`.
* Exported histograms include `count`, `sum`, `min`, `max`, `avg` and `quantile` data just like in Finagle
* A link is included on the Admin Ui to the exported data

## Usage

SBT can depend on sources from git repositories, see the example below.

``` sbt
import sbt._

object MyBuild extends Build {

  lazy val myProject = Project("myProject", file("."))
                    .dependsOn(twitter-server-prometheus)

  lazy val twitter-server-prometheus = RootProject(uri("git://github.com/kovszilard/twitter-server-prometheus.git#0.1"))

}
```

Once you have the SBT dependency, you can mix in the `PrometheusExporter` trait to your App.

```
object MyApp extends TwitterServer with PrometheusExporter {
  ...
}
```
