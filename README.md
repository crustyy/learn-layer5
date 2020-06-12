
<p style="text-align:center;" align="center">
  <img align="center" src="https://raw.githubusercontent.com/layer5io/layer5/master/assets/images/layer5/layer5-tag-white-bg.png" width="45%" /></p>

![GitHub contributors](https://img.shields.io/github/contributors/layer5io/layer5.svg)
![GitHub](https://img.shields.io/github/license/layer5io/layer5.svg) 
[![Docker Pulls](https://img.shields.io/docker/pulls/layer5/learn-layer5.svg)](https://hub.docker.com/r/layer5/learn-layer5)
[![Go Report Card](https://goreportcard.com/badge/github.com/layer5io/learn-layer5)](https://goreportcard.com/report/github.com/layer5io/learn-layer5)
[![GitHub issues by-label](https://img.shields.io/github/issues/layer5io/learn-layer5/help%20wanted.svg)](https://github.com/issues?utf8=✓&q=is%3Aopen+is%3Aissue+archived%3Afalse+org%3Alayer5io+label%3A%22help+wanted%22+")
[![Website](https://img.shields.io/website/https/layer5.io/meshery.svg)](https://layer5.io)
[![Twitter Follow](https://img.shields.io/twitter/follow/layer5.svg?label=Follow&style=social)](https://twitter.com/intent/follow?screen_name=mesheryio)
[![Slack](http://slack.layer5.io/badge.svg)](http://slack.layer5.io)
[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/3564/badge)](https://bestpractices.coreinfrastructure.org/projects/3564)

<p style="clear:both;">
<h2>Learn Layer5</h2>

The Learn Layer5 sample application is to be available for use across all service meshes that Meshery supports and is to used as:

- a learning device (for [service mesh workshops](https://layer5.io/workshops))
- for [Service Mesh Interface conformance](https://docs.google.com/document/d/1HL8Sk7NSLLj-9PRqoHYVIGyU6fZxUQFotrxbmfFtjwc/edit#)

## Application Architecture
The Learn Layer5 application includes three services: `app-a`, `app-b`, and `app-c`. Each service is listening on port `9091/tcp`.

### Service

The following are the routes defined by the `service` app and their functionality.

#### POST /call

This is the route whose metrics will be collected by the app. This route can be used to make the service call any other web service.

Simple POST request
```shell
# Command
curl --location --request POST 'http://localhost:9091/call' \
--data-raw ''
# No Output
```

`service` makes a POST request to `"http://httpbin.org/post"`.
```shell
# Command
curl --location --request POST 'http://localhost:9091/call' \
--header 'Content-Type: application/json' \
--data-raw '{
"host": "http://httpbin.org/post",
"body": "{\n\t\"hello\": \"bye\"\n}"
}'
# Output
{
  "args": {}, 
  "data": "{\n\t\"hello\": \"bye\"\n}", 
  "files": {}, 
  "form": {}, 
  "headers": {
    "Accept-Encoding": "gzip", 
    "Content-Length": "19", 
    "Content-Type": "application/json", 
    "Host": "httpbin.org", 
    "User-Agent": "Go-http-client/1.1", 
  }, 
  "json": {
    "hello": "bye"
  }, 
  "origin": "...", 
  "url": "http://httpbin.org/post"
}
```

`service` makes a get request (as body is not provided) to `http://httpbin.org/get`.
```shell
# Command
curl --location --request POST 'http://localhost:9091/call' \
--header 'Content-Type: application/json' \
--data-raw '{
"host": "http://httpbin.org/get",
}'
# Output
{
  "args": {}, 
  "headers": {
    "Accept-Encoding": "gzip", 
    "Host": "httpbin.org", 
    "User-Agent": "Go-http-client/1.1", 
  }, 
  "origin": "...", 
  "url": "http://httpbin.org/get"
}
```

#### GET /metrics

Gets the metrics from `service`
```shell
# Command
curl --location --request GET 'localhost:9091/metrics' \
--header 'Content-Type: application/json' \
--data-raw '{
"hello": "bye"
}'
# Output
{
    "requestsReceived": "19", # Total requests service recieved
    "responsesFailed": "3",   # The responses of the requests the service made that failed
    "responsesSucceeded": "7" # The responses of the requests the service made that succeeded
}
```

#### DELETE /metrics

Clears the counters in `service`
```shell
# Command
curl --location --request DELETE 'localhost:9091/metrics' \
--header 'Content-Type: application/json' \
--data-raw '{
	"hello": "bye"
}'
# No Output
```

<br /><br /><p align="center"><i>If you’re using Learn Layer5 or if you like the project, please <a href="https://github.com/layer5io/meshery/stargazers">★</a> star this repository to show your support! 🤩</i></p>
</p>

<p style="clear:both;">
<h2><a name="contributing"></a><a name="community"></a> <a href="http://slack.layer5.io">Community</a> and <a href="https://github.com/layer5io/layer5/blob/master/CONTRIBUTING.md">Contributing</a></h2>
Our projects are community-built and welcome collaboration. 👍 Be sure to see the <a href="https://docs.google.com/document/d/17OPtDE_rdnPQxmk2Kauhm3GwXF1R5dZ3Cj8qZLKdo5E/edit">Meshery Contributors Welcome Guide</a> for a tour of resources available to you and jump into our <a href="http://slack.layer5.io">Slack</a>! Contributors are expected to adhere to the <a href="https://github.com/cncf/foundation/blob/master/code-of-conduct.md">CNCF Code of Conduct</a>.

<a href="https://meshery.io/community"><img alt="Layer5 Service Mesh Community" src="img/readme/slack-128.png" style="margin-left:10px;padding-top:5px;" width="110px" align="right" /></a>

<a href="http://slack.layer5.io"><img alt="Layer5 Service Mesh Community" src="img/readme/community.svg" style="margin-right:8px;padding-top:5px;" width="140px" align="left" /></a>

<p>
✔️ <em><strong>Join</strong></em> <a href="https://drive.google.com/open?id=1c07UO9dS7_tFD-ClCWHIrEzRnzUJoFQ10EzfJTpS7FY">weekly community meeting</a> on <a href="https://bit.ly/2SbrRhe">Fridays from 10am - 11am Central</a>.<br />
✔️ <em><strong>Watch</strong></em> community <a href="https://www.youtube.com/channel/UCFL1af7_wdnhHXL1InzaMvA?sub_confirmation=1">meeting recordings</a>.<br />
✔️ <em><strong>Access</strong></em> the <a href="https://drive.google.com/drive/u/4/folders/0ABH8aabN4WAKUk9PVA">community drive</a>.<br />
</p>
<p align="center">
<i>Not sure where to start?</i> Grab an open issue with the <a href="https://github.com/issues?utf8=✓&q=is%3Aopen+is%3Aissue+archived%3Afalse+org%3Alayer5io+label%3A%22help+wanted%22+">help-wanted label</a>.
</p>

## About Layer5

**Community First**
<p>The <a href="https://layer5.io">Layer5</a> community represents the largest collection of service mesh projects and their maintainers in the world.</p>

**Open Source First**
<p>We build projects to provide learning environments, deployment and operational best practices, performance benchmarks, create documentation, share networking opportunities, and more. Our shared commitment to the open source spirit pushes Layer5 projects forward.</p>

**License**

This repository and site are available as open source under the terms of the [Apache 2.0 License](https://opensource.org/licenses/Apache-2.0).
