# test in rails


```bash
bin/rails test        # Runs all tests in test folder except system ones
bin/rails test:system # Run system tests only

bin/rails test test/system/users_test.rb
bin/rails test test/controllers/users_controller_test.rb
```