# yslow-node

A "fork" of just the node package `yslow` under the family of projects located in https://github.com/marcelduran/yslow. Unfortunately, I can't provide any of the original project's git history here (without significant effort), as all of the yslow projects are located under one large directory. I simply copied the node package out of it, and have started with a fresh commit history.

See https://github.com/marcelduran/yslow/pull/155 for the reasoning behind the decision to create this project.

# Installation

    npm install yslow-node -g

# Help

    yslow-node --help

```
Usage: yslow-node [options] [file ...]

  Options:

    -h, --help               output usage information
    -V, --version            output the version number
    -i, --info <info>        specify the information to display/log (basic|grade|stats|comps|all) [basic]
    -f, --format <format>    specify the output results format (json|xml|plain) [json]
    -r, --ruleset <ruleset>  specify the YSlow performance ruleset to be used (ydefault|yslow1|yblog) [ydefault]
    -b, --beacon <url>       specify an URL to log the results
    -d, --dict               include dictionary of results fields
    -v, --verbose            output beacon response information

  Examples:

    yslow-node file.har
    yslow-node -i grade -f xml -b http://server.com/beacon file1.har file2.har
    yslow-node --info all --format plain /tmp/*.har
    yslow-node -i basic --rulseset yslow1 -d < file.har
    curl example.com/file.har | yslow -i grade -b http://server.com/beacon -v

  More Info:

     https://yslow.org/user-guide/#version2
```

# As a module

    node

```js
> require('fs').readFile('example.com.har', function (err, data) {
    var har = JSON.parse(data),
        YSLOW = require('yslow-node').YSLOW,
        doc = require('jsdom').jsdom(),
        res = YSLOW.harImporter.run(doc, har, 'ydefault'),
        content = YSLOW.util.getResults(res.context, 'basic');

    console.log(content);
});
{ w: 98725, o: 89, u: 'http%3A%2F%2Fexample.com%2F', r: 9, i: 'ydefault', lt: 981 }
```
