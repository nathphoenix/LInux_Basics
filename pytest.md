pytest run all the test either with failure or not
pytest -x : this will run all test until it fails and it stop immediately

TESTING USING THE NODE VALUE

1. In order to run test from a particular class and exclude other class:
path_to_test :: test_class_name
example pytest data/test_string.py :: Test_class


2. In order to run unit test or test a function only, from a particular class :
path_to_test :: test_class_name :: test_function_name
example pytest data/test_string.py :: Test_class :: test_int_text

RUNNING TEST USING KEYWORDS
testsplittraining for pattern matching, it will look for test whose name is similar

pytest -k testsplittraining
