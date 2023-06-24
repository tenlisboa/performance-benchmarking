# performance-benchmarking
This is a repo with some tools and tips for performance benchmarking in NodeJS applications.

## Benchmarking Tools
There is a lib called [benchmark](https://www.npmjs.com/package/benchmark) that can be used to benchmark functions. It is very easy to use and it is very useful to compare different implementations of the same function.

```js
const Benchmark = require('benchmark');

const suite = new Benchmark.Suite;

suite
  .add('RegExp#test', function() {
    /o/.test('Hello World!');
  })
  .add('String#indexOf', function() {
    'Hello World!'.indexOf('o') > -1;
  })
  .on('cycle', function(event) {
    console.log(String(event.target));
  })
  .on('complete', function() {
    console.log('Fastest is ' + this.filter('fastest').map('name'));
  })
  .run({ 'async': true });
```

## Memory Leak Tools

### climem
[Climem](https://github.com/mcollina/climem) is a command line tool to check the memory usage of a process. It is very easy to use and it is very useful to check if there is a memory leak in a process.

```bash
$ npm install -g climem
```
Run your app setting a environment variable called CLIMEM with the port number that you want to use:
```bash
CLIMEM=8999 node app.js
```
Then you can check the memory usage of your app:
```bash
$ climem 8999
```

### Autocannon
[Autocannon](https://github.com/mcollina/autocannon) is a command line tool to check the performance of a HTTP server. It is very easy to use and it is very useful to check if there is a performance issue in a HTTP server.

```bash
$ npm install -g autocannon
```
Run your app:
```bash
node app.js
```
Then you can check the performance of your app:
```bash
$ autocannon http://localhost:3000
```
You can pass arguments to autocannon to change the number of connections, pipelining factor, duration, etc. For more information check the [usage guide](https://github.com/mcollina/autocannon#usage)

### 0x

[0x](https://www.npmjs.com/package/0x) is a command line tool to profile Node.js applications. It is very easy to use and it is very useful to check if there is a performance issue in a Node.js application.

```bash
$ npm install -g 0x
```
Run your app:
```bash
node app.js
```
Then you can check the performance of your app:
```bash
$ 0x -o ./profile node app.js
```

### Clinic

[Clinic](https://clinicjs.org/) is a suite of tools to help diagnose and pinpoint Node.js performance issues. It is very easy to use and it is very useful to check if there is a performance issue in a Node.js application.

```bash
$ npm install -g clinic
```

#### Doctor

[Doctor](https://clinicjs.org/doctor/) is a tool to help diagnose performance issues in your application and guides you towards more specialised tools to look deeper into your specific issues..

```bash
$ clinic doctor -- node app.js
```

#### Flame

[Flame](https://clinicjs.org/flame/) is a tool to flamegraphs that are a visualization of profiled software, allowing the most frequent code-paths to be identified quickly and accurately.  It primarily visualizes two metrics. The amount of time a function was on CPU, and the amount of time a function top of stack.

```bash
$ clinic flame -- node app.js
```

#### Bubbleprof

[Bubbleprof](https://clinicjs.org/bubbleprof/) is a completely new way to visualize the operation of your Node.js processes. It observes the async operations of your application, groups them, measures their delays, and draws a map of the delays in your application's async flow.

```bash
$ clinic bubbleprof -- node app.js
```

#### Heapprofile

[Heapprofiler](https://clinicjs.org/heapprofiler/) The flamegraph is an aggregated visualization of memory allocated over time. Each block represents the amount of memory allocated by a function. The wider the block, the more memory was allocated..

```bash
$ clinic heapprofile -- node app.js
```
## Tips and Advices
- Consider if the app is close to the end customer, and define a acceptable response time for the end customer and work around that.
- Run tests in a isolated machine, you can use a VM or a container. There are tones of tools to do that, like [Vagrant](https://www.vagrantup.com/) or [Docker](https://www.docker.com/).
- Always remember that beyond giving a report of the performance of your app, you need to understand the report and take actions to improve the performance of your app.
