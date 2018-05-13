# Sample Guard Auto Testing

This is a sample python project to demonstrate how you can run tests automatically
whenever there is a change in the source file or its associated test file.

[Guard](https://github.com/guard/guard) is an amazing framework written in the 
[most amazing language](https://www.ruby-lang.org/en/) (in my opinion) that lets you 
watch for file changes and run any commands on those files. It has a plethora of [plugins](https://github.com/guard/guard/wiki/Guard-Plugins) too.

There is a plugin called [guard-pytest](https://github.com/kazufusa/guard-pytest) for running python test but there is 
[no support](https://github.com/kazufusa/guard-pytest/issues/3) for desktop notifications which makes Guard awesome to use.

So I am going with a plugin called [guard-yield](https://github.com/guard/guard-yield), which you write ruby code in Guardfile itself,
to autotest python code and raise notifications using [terminal-notifier](https://github.com/julienXX/terminal-notifier) in my Mac.

You can tweak this file to run tests or whatever in your project in any language and change the notification system as per your OS.

## Project Structure

```
.
├── Gemfile
├── Guardfile
├── README.md
├── requirements.txt
├── source_dir1
│   ├── add.py
│   ├── sub_source_dir1
│   │   ├── sub.py
│   │   └── tests
│   │       └── test_sub.py
│   └── tests
│       └── test_add.py
└── source_dir2
    ├── mul.py
    └── tests
        └── test_mul.py
```

The project is structured in a way that each source file will have its associated test file under `tests` subdirectory of file's current directory. It might be different for you.

The `requirements.txt` contains the python dependency requirements.

The `Gemfile` contains the ruby dependencies for our autotesting to work.

Finally the `Guardfile` that contains the DSL for watching file changes, running tests and raise notifications. Check the file for inline comments on how it works.


## How to run this project?

1. Check out this project in a local directory
2. Run `pip install -r requirements.txt` to install pytest.
3. Test the project by running `pytest` if you want.
4. Run `bundle` to install Guard and its dependencies from the Gemfile
5. Run `bundle exec guard` to start Guard in a terminal.
6. You can hit Enter to run all tests and see the notification.
7. Or you can change some source or test files to trigger the autotesting of that file.

Note that if you are using IntelliJ, you need to be aware of [when it triggers the autosave](https://www.jetbrains.com/help/idea/saving-and-reverting-changes.html). You might change the file but IntelliJ won't immediately save the file if you are in the same frame.

You can always hit `⌘ S` to force save the file so Guard can be alerted quickly.

Suggestions and criticisms are welcome.

Thanks to all the projects linked above for the knowledge and inspiration.


