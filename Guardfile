require 'terminal-notifier'

# Run `bundle` for the first time in your terminal to install the dependencies
# Then run `bundle exec guard` in terminal for auto-running the tests


#clearing :on          # clears terminal



# Run the tests on specified files or all files
# Change the command according to your framework

def run_tests(files = nil)
    system("py.test", "-q", "--color=yes", *files)
end


# Code for notification. Change the :activate if you don't use iTerm
def notify_result(files, result)
    status = result ? 'pass' : 'fail'

    message = if files.nil?
        "Tests #{status}ed for all files!"
    else
        file = files[0][/([^\/]+)$/, 1]
        "Tests #{status}ing for #{file} !"
    end

    title = result ? '💪😎' : '😱🤯'
    TerminalNotifier.notify(message, :group => Process.pid, :title => title, :activate => 'com.googlecode.iterm2')
end


run_py_test = proc do |_guard, _command, files|
    puts "Running tests on " + (files.nil? ? "all files" : files.join(' '))
    result = run_tests(files)
    notify_result(files, result)
end


cmds = %i(run_all run_on_additions run_on_modifications run_on_removals)



guard :yield, cmds.product([run_py_test]).to_h do

    # Look for changes in files matching this pattern
    watch(%r{^(?<dir>.*)/(?<filename>[^/]*\.py)$}) { |m|

        # Run tests for files matching this pattern
        if (m[:filename].start_with?('test_'))
            "#{m[:dir]}/#{m[:filename]}"               # if it's the test file, just run this file.
        else
            test_file = "#{m[:dir]}/tests/test_#{m[:filename]}"    # if it's the source file, run the associated test file.
            File.file?(test_file) ? test_file : nil
        end

    }

end
