附件：

[rootcloud-dev-env.zip](../youdaonote-attachments/WEBRESOURCE2fe120e0f6fd747a71553191c91662b8rootcloud-dev-env.zip)



[test-demo.zip](../youdaonote-attachments/WEBRESOURCEc64c34edc95cd2e3a404ece57e8dcfaftest-demo.zip)



[tide-test.zip](../youdaonote-attachments/WEBRESOURCEc880375e3e9fe3e6d43f7fc45598d8d7tide-test.zip)



```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"value":"describe"},{"value":"用例集"},{},{"value":"it"},{"value":"具体用例"},{},{"value":"同步测试"},{"value":"用例函数执行完毕后，mocha就直接开始执行下一个用例函数","inlineStyles":{"font-size":[{"from":0,"to":29,"value":15}],"back-color":[{"from":0,"to":29,"value":"#ffffff"}]}},{"value":"同步任务指的是，在主线程上排队执行的任务，只有前一个任务执行完毕，才能执行后一个任务；","inlineStyles":{"bold":[{"from":0,"to":43,"value":true}],"font-family":[{"from":0,"to":43,"value":"Verdana"}],"color":[{"from":0,"to":43,"value":"#333333"}]}},{"value":"异步测试"},{"value":"在用例函数里边加一个done回调，异步代码执行完毕后调用一下done，就会通知mocha，我执行完了，可以执行下一个用例函数","inlineStyles":{"font-size":[{"from":0,"to":62,"value":15}],"back-color":[{"from":0,"to":62,"value":"#ffffff"}]}},{"value":"异步任务指的是，不进入主线程、而进入\"任务队列\"（task queue）的任务，只有等主线程任务执行完毕，\"任务队列\"开始通知主线程，请求执行任务，该任务才会进入主线程执行。","inlineStyles":{"bold":[{"from":0,"to":87,"value":true}],"font-family":[{"from":0,"to":87,"value":"Verdana"}],"color":[{"from":0,"to":87,"value":"#333333"}]}},{"value":"this.retries(4)"},{"value":"可放在describe里，当test fail时，可以re-execute","inlineStyles":{"font-family":[{"from":0,"to":37,"value":"Tahoma"}]}},{},{"value":"this.slow(1000)"},{"value":"可放在describe里，指定当执行时间超过1000，才提示slow","inlineStyles":{"font-family":[{"from":0,"to":34,"value":"Tahoma"}]}},{},{},{},{},{},{},{},{},{},{}],"heights":[27,25,40,40,40,40,40,40,40],"widths":[206.66666666666666,206.66666666666666,206.66666666666666]}
```





```javascript

Run tests with Mocha

Rules & Behavior
  --allow-uncaught           Allow uncaught errors to propagate        [boolean]
  --async-only, -A           Require all tests to use a callback (async) or
                             return a Promise                          [boolean]
  --bail, -b                 Abort ("bail") after first test failure   [boolean]
  --check-leaks              Check for global variable leaks           [boolean]
  --delay                    Delay initial execution of root suite     [boolean]
  --exit                     Force Mocha to quit after tests complete  [boolean]
  --forbid-only              Fail if exclusive test(s) encountered     [boolean]
  --forbid-pending           Fail if pending test(s) encountered       [boolean]
  --global, --globals        List of allowed global variables            [array]
  --retries                  Retry failed tests this many times         [number]
  --slow, -s                 Specify "slow" test threshold (in milliseconds)
                                                          [string] [default: 75]
  --timeout, -t, --timeouts  Specify test timeout threshold (in milliseconds)
                                                        [string] [default: 2000]
  --ui, -u                   Specify user interface    [string] [default: "bdd"]

Reporting & Output
  --color, -c, --colors                     Force-enable color output  [boolean]
  --diff                                    Show diff on failure
                                                       [boolean] [default: true]
  --full-trace                              Display full stack traces  [boolean]
  --growl, -G                               Enable Growl notifications [boolean]
  --inline-diffs                            Display actual/expected differences
                                            inline within each string  [boolean]
  --reporter, -R                            Specify reporter to use
                                                      [string] [default: "spec"]
  --reporter-option, --reporter-options,    Reporter-specific options
  -O                                        (<k=v,[k1=v1,..]>)           [array]

Configuration
  --config   Path to config file           [string] [default: (nearest rc file)]
  --opts     Path to `mocha.opts` (DEPRECATED)
                                         [string] [default: "./test/mocha.opts"]
  --package  Path to package.json for config                            [string]

File Handling
  --extension          File extension(s) to load
                                           [array] [default: ["js","cjs","mjs"]]
  --file               Specify file(s) to be loaded prior to root suite
                       execution                       [array] [default: (none)]
  --ignore, --exclude  Ignore file(s) or glob pattern(s)
                                                       [array] [default: (none)]
  --recursive          Look for tests in subdirectories                [boolean]
  --require, -r        Require module                  [array] [default: (none)]
  --sort, -S           Sort test files                                 [boolean]
  --watch, -w          Watch files in the current working directory for changes
                                                                       [boolean]
  --watch-files        List of paths or globs to watch                   [array]
  --watch-ignore       List of paths or globs to exclude from watching
                                      [array] [default: ["node_modules",".git"]]

Test Filters
  --fgrep, -f   Only run tests containing this string                   [string]
  --grep, -g    Only run tests matching this string or regexp           [string]
  --invert, -i  Inverts --grep and --fgrep matches                     [boolean]

Positional Arguments
  spec  One or more files, directories, or globs to test
                                                     [array] [default: ["test"]]

Other Options
  --help, -h         Show usage information & exit                     [boolean]
  --version, -V      Show version number & exit                        [boolean]
  --list-interfaces  List built-in user interfaces & exit              [boolean]
  --list-reporters   List built-in reporters & exit                    [boolean]


```











关于schema校验：

```javascript
schema = Joi.object().keys({
    app_id: Joi.string().required(),
    env: Joi.string().valid("Yes", "No").required()
});//env仅接受是/否两个范围，使用valid

//有多个可变范围 alternatives
id: Joi.alternatives()
    .try(Joi.number(), Joi.string())
    .required()

//允许空字符串和null
let schema = Joi.object({
  name : Joi.string().allow(...[null, ""]),
});
//允许empty，语法解释
any.empty(schema)
Considers anything that matches the schema to be empty (undefined)
//示例
let schema = Joi.object({
  name : Joi.string().empty(""),
});

```



