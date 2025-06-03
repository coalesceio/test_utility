<h1 align="center">test-utility</h1>
<p align="center">
</p>

<hr/>

<p align="center">
<a alt="License"
        href="https://github.com/coalesceio/test_utility/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg" /></a>

</p>

## About

`test-utility` is an extension package for [**Coalesce**], inspired by the [Great Expectations package for Python](https://greatexpectations.io/). The intent is to allow Coalesce users to deploy GE-like tests in their data warehouse directly from Coalesce, vs having to add another integration with their data warehouse.


## How to use?

Step 1: Once you install this package from Coalesce marketplace then you will need to import this package to workspace macro.

Assuming the alias you gave the package is TestUtility you would add the below Jinja.  `testUtils` could be anything.  You will use this alias to reference test macros in the imported package.

```yaml
{% import "TestUtility" as testUtils with context %}
```

![image](https://github.com/user-attachments/assets/62d6075d-f1cb-4b90-818e-b2a1c79285dc)


Step 2: Open a Node for which you want to create a test case.

Step 3: Goto Testing Configuration.

Step 4: Click on 'New Test' button.


![image](https://github.com/user-attachments/assets/dcc56a4b-5f89-49e8-be24-ee0deaa6a099)


Step 5: You will see new test case added for the Node.

![image](https://github.com/user-attachments/assets/aab2130d-9bbe-43f0-91b5-b1ae592bf842)


Step 6: In the text field, call the macro using the package import alias followed by a dot and the test case name.
        
_For Example, I am trying to Run Test case, 'expect_table_row_count_to_be_between' from the avilable test below._
        
![image](https://github.com/user-attachments/assets/4c546eb2-7b66-4e41-b514-99da676993a6)



Step 7: Replace the input parameters in macro call as per requirment.

_In this test case 'group_by' and 'filterCondition' inputs are optional, so i am ignoring here._

![image](https://github.com/user-attachments/assets/febcfc74-68dd-4447-a28a-94fb6b350935)



Note - You can refer object name with all the avilable pattern in Coalesce.  For example, [ref_no_link()](https://docs.coalesce.io/docs/reference/ref-functions/#ref_no_link) may be used instead of [this](https://docs.coalesce.io/docs/reference/ref-functions/#this).

Step 8: You can execute this test case using 'Run' button.


## Example

Lets consider, i have one table with named, TEST_TABLE. 

1. I want to check if each column value to be in a given set.
   _I will refer test case expect_column_values_to_be_in_set for this scenario. And my test case systax will be_
```yaml
   {{ testUtils.expect_column_values_to_be_in_set( 'CONTACT_VIA', ['EMAIL','CALL','TEXT']) }}
```

2. I want to check if each column entries to be strings that match a given SQL like pattern.
   _I will refer test case expect_column_values_to_match_like_pattern for this scenario. And my test case systax will be_
```yaml
   {{ testUtils.expect_column_values_to_match_like_pattern('{{ 'EMAIL_ID', '%@%') }}
```

## Available Tests

### Table shape

- [expect_column_to_exist](#expect_column_to_exist)
- [expect_row_values_to_have_recent_data](#expect_row_values_to_have_recent_data)
- [expect_grouped_row_values_to_have_recent_data](#expect_grouped_row_values_to_have_recent_data)
- [expect_table_aggregation_to_equal_other_table](#expect_table_aggregation_to_equal_other_table)
- [expect_table_column_count_to_be_between](#expect_table_column_count_to_be_between)
- [expect_table_column_count_to_equal_other_table](#expect_table_column_count_to_equal_other_table)
- [expect_table_column_count_to_equal](#expect_table_column_count_to_equal)
- [expect_table_columns_to_not_contain_set](#expect_table_columns_to_not_contain_set)
- [expect_table_columns_to_contain_set](#expect_table_columns_to_contain_set)
- [expect_table_columns_to_match_ordered_list](#expect_table_columns_to_match_ordered_list)
- [expect_table_columns_to_match_set](#expect_table_columns_to_match_set)
- [expect_table_row_count_to_be_between](#expect_table_row_count_to_be_between)
- [expect_table_row_count_to_equal_other_table](#expect_table_row_count_to_equal_other_table)
- [expect_table_row_count_to_equal_other_table_times_factor](#expect_table_row_count_to_equal_other_table_times_factor)
- [expect_table_row_count_to_equal](#expect_table_row_count_to_equal)

### Missing values, unique values, and types

- [expect_column_values_to_be_of_type](#expect_column_values_to_be_of_type)
- [expect_column_values_to_be_in_type_list](#expect_column_values_to_be_in_type_list)
- [expect_column_values_to_have_consistent_casing](#expect_column_values_to_have_consistent_casing)

### Sets and ranges

- [expect_column_values_to_be_in_set](#expect_column_values_to_be_in_set)
- [expect_column_values_to_not_be_in_set](#expect_column_values_to_not_be_in_set)
- [expect_column_values_to_be_between](#expect_column_values_to_be_between)
- [expect_column_values_to_be_decreasing](#expect_column_values_to_be_decreasing)
- [expect_column_values_to_be_increasing](#expect_column_values_to_be_increasing)

### String matching

- [expect_column_value_lengths_to_be_between](#expect_column_value_lengths_to_be_between)
- [expect_column_value_lengths_to_equal](#expect_column_value_lengths_to_equal)
- [expect_column_values_to_match_like_pattern](#expect_column_values_to_match_like_pattern)
- [expect_column_values_to_match_like_pattern_list](#expect_column_values_to_match_like_pattern_list)
- [expect_column_values_to_match_regex](#expect_column_values_to_match_regex)
- [expect_column_values_to_match_regex_list](#expect_column_values_to_match_regex_list)
- [expect_column_values_to_not_match_like_pattern](#expect_column_values_to_not_match_like_pattern)
- [expect_column_values_to_not_match_like_pattern_list](#expect_column_values_to_not_match_like_pattern_list)
- [expect_column_values_to_not_match_regex](#expect_column_values_to_not_match_regex)
- [expect_column_values_to_not_match_regex_list](#expect_column_values_to_not_match_regex_list)

### Aggregate functions

- [expect_column_distinct_count_to_be_greater_than](#expect_column_distinct_count_to_be_greater_than)
- [expect_column_distinct_count_to_be_less_than](#expect_column_distinct_count_to_be_less_than)
- [expect_column_distinct_count_to_equal_other_table](#expect_column_distinct_count_to_equal_other_table)
- [expect_column_distinct_count_to_equal](#expect_column_distinct_count_to_equal)
- [expect_column_distinct_values_to_be_in_set](#expect_column_distinct_values_to_be_in_set)
- [expect_column_distinct_values_to_contain_set](#expect_column_distinct_values_to_contain_set)
- [expect_column_distinct_values_to_equal_set](#expect_column_distinct_values_to_equal_set)
- [expect_column_max_to_be_between](#expect_column_max_to_be_between)
- [expect_column_mean_to_be_between](#expect_column_mean_to_be_between)
- [expect_column_median_to_be_between](#expect_column_median_to_be_between)
- [expect_column_min_to_be_between](#expect_column_min_to_be_between)
- [expect_column_most_common_value_to_be_in_set](#expect_column_most_common_value_to_be_in_set)
- [expect_column_proportion_of_unique_values_to_be_between](#expect_column_proportion_of_unique_values_to_be_between)
- [expect_column_quantile_values_to_be_between](#expect_column_quantile_values_to_be_between)
- [expect_column_stdev_to_be_between](#expect_column_stdev_to_be_between)
- [expect_column_sum_to_be_between](#expect_column_sum_to_be_between)
- [expect_column_unique_value_count_to_be_between](#expect_column_unique_value_count_to_be_between)

### Multi-column

- [expect_column_pair_values_A_to_be_greater_than_B](#expect_column_pair_values_a_to_be_greater_than_b)
- [expect_column_pair_values_to_be_equal](#expect_column_pair_values_to_be_equal)
- [expect_column_pair_values_to_be_in_set](#expect_column_pair_values_to_be_in_set)
- [expect_compound_columns_to_be_unique](#expect_compound_columns_to_be_unique)
- [expect_multicolumn_sum_to_equal](#expect_multicolumn_sum_to_equal)
- [expect_select_column_values_to_be_unique_within_record](#expect_select_column_values_to_be_unique_within_record)

### Distributional functions

- [expect_column_values_to_be_within_n_moving_stdevs](#expect_column_values_to_be_within_n_moving_stdevs)
- [expect_column_values_to_be_within_n_stdevs](#expect_column_values_to_be_within_n_stdevs)


## Documentation

### [expect_column_to_exist]

Expect the specified column to exist.

*Applies to:* Column

```yaml
tests: {{ expect_column_to_exist( 'columnName') }}
```

### [expect_row_values_to_have_recent_data]

Expect the model to have rows that are at least as recent as the defined interval prior to the current timestamp. Optionally gives the possibility to apply filters on the results.

*Applies to:* Column

```yaml
tests: {{ expect_row_values_to_have_recent_data( 'columnName', 'datePart_', 'interval_', row_condition = None) }}

Inputs: datepart_ = 'day'
        interval_ = '1'
        row_condition = 'id is not null' #optional
```

### [expect_grouped_row_values_to_have_recent_data] 

Expect the model to have **grouped** rows that are at least as recent as the defined interval prior to the current timestamp.
Use this to test whether there is recent data for each grouped row defined by `group_by` (which is a list of columns) and a `timestamp_column`. Optionally gives the possibility to apply filters on the results.

*Applies to:* Object

```yaml
tests : {{ expect_grouped_row_values_to_have_recent_data(group_by,timestamp_column,datepart,interval,filterCondition=None ) }}

Inputs: group_by = ['group_id', 'other_group_id']
        timestamp_column = 'date_day'
        datepart = day
        interval = 1
        filterCondition = "id is not null" #optional
```

### [expect_table_aggregation_to_equal_other_table]

Expect an (optionally grouped) expression to match the same (or optionally other) expression in a different table.

*Applies to:* Object

Simple Test:

```yaml
tests: {{ expect_table_aggregation_to_equal_other_table(expression,compare_model,group_by=None) }}

Inputs: expression = sum(col_numeric_a)
        compare_model = ref("other_model")
        group_by = [idx] #optional
```

More complex Test:

```yaml
tests: {{ expect_table_aggregation_to_equal_other_table(
          expression,
          compare_model,compare_expression=None,
          group_by=None,compare_group_by=None,
          row_condition=None,compare_row_condition=None,
          tolerance=0.0,tolerance_percent=None ) }}

Inputs: expression = 'max("column_a")'
        compare_model = 'ref("other_model")'
        compare_expression = 'max("column_b")'
        group_by = ['date_column']
        compare_group_by = ['some_other_date_column']
        row_condition = 'some_flag=true'
        compare_row_condition = 'some_flag=false'

```

**Note**: You can also express a **tolerance** factor, either as an absolute tolerable difference, `tolerance`, or as a tolerable % difference `tolerance_percent` expressed as a decimal (i.e 0.05 for 5%).

### [expect_table_column_count_to_be_between]

Expect the number of columns in a model to be between two values.

*Applies to:* Object

```yaml
tests: {{ expect_table_column_count_to_be_between( minValue , maxValue) }}
Inputs: minValue = 1
        maxValue = 4 
```

### [expect_table_column_count_to_equal_other_table]

Expect the number of columns in a model to match another model.

*Applies to:* Object

```yaml
tests: {{ expect_table_column_count_to_equal_other_table( 'comparing_tableName') }}

```

### [expect_table_columns_to_not_contain_set]

Expect the columns in a model not to contain a given list.

*Applies to:* Object

```yaml
tests: {{ expect_table_columns_to_not_contain_set( notExpectedColumnList) }}
Inputs: notExpectedColumnList = ["col_a", "col_b"]
```

### [expect_table_columns_to_contain_set]

Expect the columns in a model to contain a given list.

*Applies to:* Object

```yaml
tests: {{ expect_table_columns_to_contain_set( ExpectedColumnList) }}
Inputs: ExpectedColumnList = ["col_a", "col_b"]

```

### [expect_table_column_count_to_equal]

Expect the number of columns in a model to be equal to `expected_number_of_columns`.

*Applies to:* Object

```yaml
tests: {{ expect_table_column_count_to_equal( ExpectedCount ) }}
Inputs: ExpectedCount = '7'
```

### [expect_table_columns_to_match_ordered_list]

Expect the columns to exactly match a specified list.

*Applies to:* Object

```yaml
tests: {{ expect_table_columns_to_match_ordered_list( column_list, transform="UPPER") }}

Inputs:   column_list = ["col_a", "col_b"]
          transform = upper # (Optional)
```

### [expect_table_columns_to_match_set]

Expect the columns in a model to match a given list.

*Applies to:* Object

```yaml
tests: {{ expect_table_columns_to_match_set( ExpectedColumnList) }}

Inputs: column_list = ["col_a", "col_b"]
```

### [expect_table_row_count_to_be_between]

Expect the number of rows in a model to be between two values.
*Applies to:* Object

```yaml
tests: {{ expect_table_row_count_to_be_between( minValue , maxValue ,group_by = None, filterCondition = None) }}

Inputs:   minValue = 1 
          maxValue = 4 
          group_by = ['group_id', 'other_group_id', ...] # (Optional)
          filterCondition: 'id is not null' # (Optional)
```

### [expect_table_row_count_to_equal_other_table]

Expect the number of rows in a model match another model.

*Applies to:* Object

```yaml
tests: {{ expect_table_row_count_to_equal_other_table( comparing_tableName, group_by_t1 = None, group_by_t2 = None,  filterCondition_t1 = None, filterCondition_t2 = None) }}

Inputs:   comparing_tableName = {{ ref('target','other_model') }}
          group_by_t1 = ['col1', 'col2'] # (Optional)
          group_by_t2 = ['col1', 'col2'] # (Optional)
          filterCondition_t1 = "id is not null" # (Optional)
          filterCondition_t2 = "id is not null" # (Optional)
```

### [expect_table_row_count_to_equal_other_table_times_factor]

Expect the number of rows in a model to match another model times a preconfigured factor.

*Applies to:* Object

```yaml
tests: {{ expect_table_row_count_to_equal_other_table_times_factor( comparing_tableName,  group_by_t1 = None, group_by_t2 = None, filterCondition_t1 = None, filterCondition_t2 = None, factor = None) }}

Inputs:   comparing_tableName = {{ ref('target','other_model') }}
          factor = '13'
          group_by_t1 = ['col1', 'col2'] # (Optional)
          group_by_t2 = ['col1', 'col2'] # (Optional)
          filterCondition_t1 = "id is not null" # (Optional)
          filterCondition_t2 = "id is not null" # (Optional)
```

### [expect_table_row_count_to_equal]

Expect the number of rows in a model to be equal to `expected_number_of_rows`.

*Applies to:* Object

```yaml
tests: {{ expect_table_row_count_to_equal( numberOfRecordExpected, group_by = None, filterCondition = None) }}

Inputs:   numberOfRecordExpected = '4'
          group_by = ['group_id', 'other_group_id', ...] # (Optional)
          filterCondition = "id is not null" # (Optional)
```

### [expect_column_values_to_be_of_type]

Expect a column to be of a specified data type.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_be_of_type( columnName, dataType) }}

Input: dataType = 'date'
```

### [expect_column_values_to_be_in_type_list]

Expect a column to be one of a specified type list.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_be_in_type_list( columnName, dataType) }}

Inputs: dataType = ['date', 'datetime']
```

### [expect_column_values_to_have_consistent_casing]

Expect a column to have consistent casing. By setting `display_inconsistent_columns` to true, the number of inconsistent values in the column will be displayed in the terminal whereas the inconsistent values themselves will be returned if the SQL compiled test is run.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_have_consistent_casing( column_name, display_inconsistent_columns=False) }}

Input: display_inconsistent_columns = false # (Optional)
```

### [expect_column_values_to_be_in_set]

Expect each column value to be in a given set.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_be_in_set( columnName, expectedValueList, filterCondition = None) }}

Inputs: expectedValueList = ['a','b','c']
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_values_to_be_between]

Expect each column value to be between two values.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_be_between( columnName, minValue , maxValue, filterCondition = None ) }}

Inputs: minValue = '0'  
        maxValue = '10' 
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_values_to_not_be_in_set]

Expect each column value not to be in a given set.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_not_be_in_set( columnName, expectedValueList, filterCondition = None) }}

Inputs: expectedValueList = ['e','f','g']
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_values_to_be_increasing]

Expect column values to be increasing.

If `strictly: True`, then this expectation is only satisfied if each consecutive value is strictly increasing – equal values are treated as failures.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_be_increasing(  column_name, sort_column=None, strictly=True, filterCondition=None, group_by=None, step=None) }}

Inputs: sort_column = date_day
        filterCondition = "id is not null" # (Optional)
        strictly = true # (Optional for comparison operator. Default is 'true', and it uses '>'. If set to 'false' it uses '>='.)
        group_by = [group_id, other_group_id, ...] # (Optional)
        step = 1 # (Optional. If set, it requires the difference between values to be exactly this step. Requires numeric columns.)
```

### [expect_column_values_to_be_decreasing]

Expect column values to be decreasing.

If `strictly=True`, then this expectation is only satisfied if each consecutive value is strictly decreasing – equal values are treated as failures.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_be_decreasing( column_name, sort_column=None, strictly=True, filterCondition=None, group_by=None, step=None) }}

Inputs: sort_column = col_numeric_a
        filterCondition = "id is not null" # (Optional)
        strictly = true # (Optional for comparison operator. Default is 'true' and it uses '<'. If set to 'false', it uses '<='.)
        group_by = [group_id, other_group_id, ...] # (Optional)
        step = 1 # (Optional. If set, it requires the difference between values to be exactly this step. Requires numeric columns.)
```

### [expect_column_value_lengths_to_be_between]

Expect column entries to be strings with length between a min_value value and a max_value value (inclusive).

*Applies to:* Column

```yaml
tests: {{ expect_column_value_lengths_to_be_between( columnName, minLength, maxLength, filterCondition = None) }}

Inputs: min_value = '1' 
        max_value = '4' 
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_value_lengths_to_equal]

Expect column entries to be strings with length equal to the provided value.

*Applies to:* Column

```yaml
tests: {{ expect_column_value_lengths_to_equal( columnName, rowsValueLength, filterCondition = None) }}

Inputs: rowsValueLength = '10'
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_values_to_match_regex]

Expect column entries to be strings that match a given regular expression. Valid matches can be found anywhere in the string, for example "[at]+" will identify the following strings as expected: "cat", "hat", "aa", "a", and "t", and the following strings as unexpected: "fish", "dog".

Optional (keyword) arguments:

- `isRaw` indicates the `regex` pattern is a "raw" string and should be escaped. The default is `False`.
- `flags` is a string of one or more characters that are passed to the regex engine as flags (or parameters). Allowed flags are adapter-specific. A common flag is `i`, for case-insensitive matching. The default is no flags.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_match_regex( columnName, regex, isRaw = False, flags='', filterCondition=None ) }}

Inputs: regex = '[at]+'
        filterCondition = 'id is not null' # (Optional)
        isRaw = 'True' # (Optional)
        flags = 'i' # (Optional)
```

### [expect_column_values_to_not_match_regex]

Expect column entries to be strings that do NOT match a given regular expression. The regex must not match any portion of the provided string. For example, "[at]+" would identify the following strings as expected: "fish”, "dog”, and the following as unexpected: "cat”, "hat”.

Optional (keyword) arguments:

- `isRaw` indicates the `regex` pattern is a "raw" string and should be escaped. The default is `False`.
- `flags` is a string of one or more characters that are passed to the regex engine as flags (or parameters). Allowed flags are adapter-specific. A common flag is `i`, for case-insensitive matching. The default is no flags.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_not_match_regex( columnName, regex, isRaw = False, flags='', filterCondition=None ) }} 

Inputs: regex = "[at]+"
        filterCondition = "id is not null" # (Optional)
        isRaw = 'True' # (Optional)
        flags = 'i' # (Optional)
```

### [expect_column_values_to_match_regex_list]

Expect the column entries to be strings that can be matched to either any of or all of a list of regular expressions. Matches can be anywhere in the string.

Optional (keyword) arguments:

- `isRaw` indicates the `regex` pattern is a "raw" string and should be escaped. The default is `False`.
- `flags` is a string of one or more characters that are passed to the regex engine as flags (or parameters). Allowed flags are adapter-specific. A common flag is `i`, for case-insensitive matching. The default is no flags.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_match_regex_list( columnName, regexList, matchType='all', isRaw=False, flags='', filterCondition=None ) }}

Inputs: regex_list = ["@[^.]*", "&[^.]*"]
        matchType = 'any' # (Optional. Default is 'all', which applies an 'AND' for each regex. If 'any', it applies an 'OR' for each regex.)
        filterCondition = "id is not null" # (Optional)
        isRaw = 'True' # (Optional)
        flags = 'i' # (Optional)
```

### [expect_column_values_to_not_match_regex_list]

Expect the column entries to be strings that do not match any of a list of regular expressions. Matches can be anywhere in the string.

Optional (keyword) arguments:

- `isRaw` indicates the `regex` pattern is a "raw" string and should be escaped. The default is `False`.
- `flags` is a string of one or more characters that are passed to the regex engine as flags (or parameters). Allowed flags are adapter-specific. A common flag is `i`, for case-insensitive matching. The default is no flags.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_not_match_regex_list( columnName, regexList, matchType='all', isRaw=False, flags='', filterCondition=None ) }} 

Inputs: regex_list = ["@[^.]*", "&[^.]*"]
        matchType = 'any' # (Optional. Default is 'all', which applies an 'AND' for each regex. If 'any', it applies an 'OR' for each regex.)
        filterCondition = "id is not null" # (Optional)
        isRaw = 'True' # (Optional)
        flags = 'i' # (Optional)
```

### [expect_column_values_to_match_like_pattern]

Expect column entries to be strings that match a given SQL `like` pattern.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_match_like_pattern( columnName, pattern, filterCondition = None) }}

Inputs: pattern = '%@%'
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_values_to_not_match_like_pattern]

Expect column entries to be strings that do not match a given SQL `like` pattern.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_not_match_like_pattern( columnName, pattern, filterCondition = None) }}

Inputs: pattern = '%&%'
        row_condition = "id is not null" # (Optional)
```

### [expect_column_values_to_match_like_pattern_list]

Expect the column entries to be strings that match any of a list of SQL `like` patterns.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_match_like_pattern_list( columnName, patternList, matchType='any', filterCondition = None) }}

Inputs: patternList = ["%@%", "%&%"]
        matchType = 'any' # (Optional. Default is 'any', which applies an 'OR' for each pattern. If 'all', it applies an 'AND' for each regex.)
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_values_to_not_match_like_pattern_list]

Expect the column entries to be strings that do not match any of a list of SQL `like` patterns.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_not_match_like_pattern_list( columnName, patternList, matchType='any', filterCondition = None) }}

Inputs: patternList = ["%@%", "%&%"]
        matchType = 'any' # (Optional. Default is 'any', which applies an 'OR' for each pattern. If 'all', it applies an 'AND' for each regex.)
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_distinct_count_to_equal]

Expect the number of distinct column values to be equal to a given value.

*Applies to:* Column

```yaml
tests: {{ expect_column_distinct_count_to_equal( columnName, expextedCount, group_by = None, filterCondition = None) }}

Inputs: value = '10'
        group_by = ['group_id', 'other_group_id', ...] # (Optional)
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_distinct_count_to_be_greater_than]

Expect the number of distinct column values to be greater than a given value.

*Applies to:* Column

```yaml
tests: {{ expect_column_distinct_count_to_be_greater_than( columnName, expextedCount, group_by = None, filterCondition = None) }}

Inputs: value = '10'
        group_by = ['group_id', 'other_group_id', ...] # (Optional)
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_distinct_count_to_be_less_than]

Expect the number of distinct column values to be less than a given value.

*Applies to:* Column

```yaml
tests: {{ expect_column_distinct_count_to_be_less_than( columnName, expextedCount, group_by = None, filterCondition = None) }}

Inputs: value = '10'
        group_by = ['group_id', 'other_group_id', ...] # (Optional)
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_distinct_values_to_be_in_set]

Expect the set of distinct column values to be contained by a given set.

*Applies to:* Column

```yaml
tests: {{ expect_column_distinct_values_to_be_in_set( columnName, expectedValueList, filterCondition = None) }}

Inputs: value_set = ['a','b','c','d']
        row_condition = "id is not null" # (Optional)
```

### [expect_column_distinct_values_to_contain_set]

Expect the set of distinct column values to contain a given set.

In contrast to `expect_column_values_to_be_in_set` this ensures not that all column values are members of the given set but that values from the set must be present in the column.

*Applies to:* Column

```yaml
tests: {{ expect_column_distinct_values_to_contain_set( columnName, expectedValueList, filterCondition = None) }}

Inputs: value_set = ['a','b']
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_distinct_values_to_equal_set]

Expect the set of distinct column values to equal a given set.

In contrast to `expect_column_distinct_values_to_contain_set` this ensures not only that a certain set of values are present in the column but that these and only these values are present.

*Applies to:* Column

```yaml
tests: {{ expect_column_distinct_values_to_equal_set( columnName, expectedValueList, filterCondition = None) }}

Inputs: value_set = ['a','b','c']
        row_condition = "id is not null" # (Optional)
```

### [expect_column_distinct_count_to_equal_other_table]

Expect the number of distinct column values to be equal to number of distinct values in another model.

*Applies to:* Column

```yaml
tests: {{ expect_column_distinct_count_to_equal_other_table( columnName, otherTableName, otherColumnName, filterCondition_t1 = None, filterCondition_t2 = None) }}

Inputs:   columnName = 'col_1'
          otherTableName = ref("my_model_2")
          otherColumnName = col_2
          filterCondition_t1 = "id is not null" # (Optional)
          filterCondition_t2 = "id is not null" # (Optional)
```


### [expect_column_mean_to_be_between]

Expect the column mean to be between a min_value value and a max_value value (inclusive).

*Applies to:* Column

```yaml
tests: {{ expect_column_mean_to_be_between( columnName, minValue, maxValue, filterCondition = None, group_by = None ) }}

Inputs: minValue = '0' 
        maxValue = '2' 
        group_by = ['group_id', 'other_group_id', ...] # (Optional)
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_median_to_be_between]

Expect the column median to be between a min_value value and a max_value value (inclusive).

*Applies to:* Column

```yaml
tests: {{ expect_column_median_to_be_between( columnName, minValue, maxValue, filterCondition = None, group_by = None ) }}

Inputs: minValue = '0'
        maxValue = '2'
        group_by = ['group_id', 'other_group_id', ...] # (Optional)
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_quantile_values_to_be_between]

Expect specific provided column quantiles to be between provided min_value and max_value values.

*Applies to:* Column

```yaml
tests: {{ expect_column_quantile_values_to_be_between( columnName, quantile, minValue , maxValue, filterCondition = None, group_by = None ) }}

Inputs: quantile = '.95'
        minValue = '0' 
        maxValue = '2' 
        group_by = ['group_id', 'other_group_id', ...] # (Optional)
        filterCondition: "id is not null" # (Optional)
```

### [expect_column_stdev_to_be_between]

Expect the column standard deviation to be between a min_value value and a max_value value. Uses sample standard deviation (normalized by N-1).

*Applies to:* Column

```yaml
tests: {{ expect_column_stdev_to_be_between( columnName, minValue, maxValue, filterCondition = None, group_by = None ) }}

Inputs: minValue = '0' 
        maxValue = '2'
        group_by = ['group_id', 'other_group_id', ...] # (Optional)
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_unique_value_count_to_be_between]

Expect the number of unique values to be between a min_value value and a max_value value.

*Applies to:* Column

```yaml
tests: {{ expect_column_unique_value_count_to_be_between( columnName, minValue, maxValue, filterCondition = None, group_by = None ) }}

Inputs: minValue = '2'
        maxValue = '2' 
        group_by = ['group_id', 'other_group_id', ...] # (Optional)
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_proportion_of_unique_values_to_be_between]

Expect the proportion of unique values to be between a min_value value and a max_value value.

For example, in a column containing [1, 2, 2, 3, 3, 3, 4, 4, 4, 4], there are 4 unique values and 10 total values for a proportion of 0.4.

*Applies to:* Column

```yaml
tests: {{ expect_column_proportion_of_unique_values_to_be_between( columnName, minValue, maxValue,  filterCondition = None, group_by = None) }}

Inputs: minValue = '0'  
        maxValue = '.4' 
        group_by = ['group_id', 'other_group_id', ...] # (Optional)
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_most_common_value_to_be_in_set]

Expect the most common value to be within the designated value set

*Applies to:* Column

```yaml
tests: {{ expect_column_most_common_value_to_be_in_set( column_name, value_set, top_n, quote_values=True, data_type="STRING", filterCondition=None) }}

Inputs: value_set: ['0.5']
        top_n: 1
        quote_values: true # (Optional. Default is 'true'.)
        data_type: "decimal" # (Optional. Default is 'decimal')
```

### [expect_column_max_to_be_between]

Expect the column max to be between a min and max value

*Applies to:* Column

```yaml
tests: {{ expect_column_max_to_be_between( columnName, minValue, maxValue, filterCondition = None, group_by = None) }}

Inputs: minValue = '1' 
        maxValue = '1' 
        group_by = ['group_id', 'other_group_id', ...] # (Optional)
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_min_to_be_between]

Expect the column min to be between a min and max value

*Applies to:* Column

```yaml
tests: {{ expect_column_min_to_be_between( columnName, minValue, maxValue, filterCondition = None, group_by = None) }}

Inputs: minValue = 0 
        maxValue = 1 
        group_by = [group_id, other_group_id, ...] # (Optional)
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_sum_to_be_between]

Expect the column to sum to be between a min and max value

*Applies to:* Column

```yaml
tests: {{ expect_column_sum_to_be_between( columnName, minValue, maxValue, filterCondition = None, group_by = None ) }}

Inputs: minValue = 1 
        maxValue = 2 
        group_by = [group_id, other_group_id, ...] # (Optional)
        row_condition = "id is not null" # (Optional)
```

### [expect_column_pair_values_A_to_be_greater_than_B]

Expect values in column A to be greater than column B.

*Applies to:* Object

```yaml
tests: {{ expect_column_pair_values_A_to_be_greater_than_B( columnNameA, columnNameB, orEqualTo = FALSE, filterCondition = None) }}

Inputs: columnNameA = 'col_numeric_a'
        columnNameB = 'col_numeric_a'
        orEqualTo = True
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_pair_values_to_be_equal]

Expect the values in column A to be the same as column B.

*Applies to:* Object

```yaml
tests: {{ expect_column_pair_values_to_be_equal( columnNameA, columnNameB, filterCondition = None) }}

Inputs: columnNameA = 'col_numeric_a'
        columnNameB = 'col_numeric_a'
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_pair_values_to_be_in_set]

Expect paired values from columns A and B to belong to a set of valid pairs.

Note: value pairs are expressed as lists within lists

*Applies to:* Object

```yaml
tests: {{ expect_column_pair_values_to_be_in_set( columnNameA, columnNameB, validPairs, filterCondition = None) }}

Inputs: column_A = 'col_numeric_a'
        column_B = 'col_numeric_b'
        value_pairs_set = [[0, 1], [1, 0], [0.5, 0.5], [0.5, 0.5]]
        filterCondition = "id is not null" # (Optional)
```

### [expect_select_column_values_to_be_unique_within_record]

Expect the values for each record to be unique across the columns listed. Note that records can be duplicated.

*Applies to:* Object

```yaml
tests: {{ expect_select_column_values_to_be_unique_within_record( column_list, filterCondition=None) }}

Inputs: column_list = ["col_string_a", "col_string_b"]
        filterCondition = "id is not null" # (Optional)
```

### [expect_multicolumn_sum_to_equal]

Expects that sum of all rows for a set of columns is equal to a specific value

*Applies to:* Object

```yaml
tests: {{ expect_multicolumn_sum_to_equal( column_list, sum_total, group_by=None, filterCondition=None) }}

Inputs: column_list = ["col_numeric_a", "col_numeric_b"]
        sum_total = 4
        group_by = [group_id, other_group_id, ...] # (Optional)
        filterCondition = "id is not null" # (Optional)
```

### [expect_compound_columns_to_be_unique]

Expect that the columns are unique together, e.g. a multi-column primary key.

*Applies to:* Object

```yaml
tests: {% macro expect_compound_columns_to_be_unique( columnNames, filterCondition = None) %}

Inputs: column_list = ["date_col", "col_string_b"]
        filterCondition = "id is not null" # (Optional)
```

### [expect_column_values_to_be_within_n_moving_stdevs]

A simple anomaly test based on the assumption that differences between periods in a given time series follow a log-normal distribution.
Thus, we would expect the logged differences (vs N periods ago) in metric values to be within Z sigma away from a moving average.
By applying a list of columns in the `group_by` parameter, you can also test for deviations within a group.

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_be_within_n_moving_stdevs(
     column_name, date_column_name, group_by=None, 
    period='day', lookback_periods=1, trend_periods=7, test_periods=14, 
    sigma_threshold=3, sigma_threshold_upper=None, sigma_threshold_lower=None, 
    take_diffs=true, take_logs=true
) }}

Inputs: date_column_name = date
        period = day # (Optional. Default is 'day')
        lookback_periods = 1 # (Optional. Default is 1)
        trend_periods = 7 # (Optional. Default is 7)
        test_periods = 14 # (Optional. Default is 14)
        sigma_threshold = 3 # (Optional. Default is 3)
        take_logs = true # (Optional. Default is 'true')
        sigma_threshold_upper = x # (Optional. Replace 'x' with a value. Default is 'None')
        sigma_threshold_lower = y # (Optional. Replace 'y' with a value. Default is 'None')
        take_diffs = true # (Optional. Default is 'true')
        group_by = [group_id] # (Optional. Default is 'None')
```

### [expect_column_values_to_be_within_n_stdevs]

Expects (optionally grouped & summed) metric values to be within Z sigma away from the column average

*Applies to:* Column

```yaml
tests: {{ expect_column_values_to_be_within_n_stdevs( column_name, group_by=None, sigma_threshold=3) }}

Inputs: group_by = ['group_id'] # (Optional. Default is 'None')
        sigma_threshold = '3' # (Optional. Default is 3)
```

### [test_missing_dates]

Check missing dates in given range.

*Applies to:* Column

```yaml
tests: {{ test_missing_dates(date_column, from, to) }}

Inputs: from = '2024-01-01' # (start of date range)
        to = '2024-01-01' # (end of date range)
```

### [test_missing_date_offset]

Check missing dates from current date to offset.

*Applies to:* Column

```yaml
tests: {{ test_missing_date_offset(date_column, from, to) }}

Inputs: from = '100' 
        to = '1' 
```
