# Date and time functions

This page describes the date and time functions and [format expressions](date-and-time-functions.md#date-format-expressions) supported in Firebolt.

## CURRENT\_DATE

Returns the current year, month and day as a `DATE` value, formatted as YYYY-MM-DD.

**Syntax**

```sql
​​CURRENT_DATE()​​
```

**Example**

```
SELECT
    CURRENT_DATE();
```

**Returns:** `2021-11-04`

## DATE\_ADD

Calculates a new `DATE `or `TIMESTAMP` by adding or subtracting a specified number of time units from an indicated expression.

**Syntax**

```sql
​​DATE_ADD('<unit>', <interval>, <date_expr>)​​
```

| Parameter     | Description                                                                                                                 |
| ------------- | --------------------------------------------------------------------------------------------------------------------------- |
| `<unit>`      | A unit of time. This can be any of the following: `SECOND`                                                                  |
| `<interval>`  | The number of times to increase the ​`<date_expr>​​` by the time unit specified by `<unit>`. This can be a negative number. |
| `<date_expr>` | An expression that evaluates to a `DATE` or `TIMESTAMP` value.                                                              |

**Examples**

The example below uses a table `date_test` with the columns and values below.

|          |            |
| -------- | ---------- |
| Category | sale\_date |
| a        | 2012-05-01 |
| b        | 2021-08-30 |
| c        | 1999-12-31 |

This example below adds 15 weeks to the `sale_date` column.

```sql
SELECT
	Category,
	DATE_ADD('WEEK', 15, sale_date)
FROM
	date_test
```

**Returns**:

```
+---+------------+
| a | 2012-08-14 |
| b | 2021-12-13 |
| c | 2000-04-14 |
+---+------------+
```

This example below subtracts 6 months from a given start date string. This string representation of a date first needs to be transformed to `DATE `type using the `CAST `function.

```
SELECT
    DATE_ADD('MONTH', -6, CAST ('2021-11-04' AS DATE));
```

**Returns**: `2021-05-04`

## DATE\_DIFF

Calculates the difference between ​​`start_date`​​ and ​`end_date`​​ by the indicated ​unit​​.

**Syntax**

```sql
​​DATE_DIFF('<unit>', <start_date>, <end_date>)​​
```

| Parameter      | Description                                                    |
| -------------- | -------------------------------------------------------------- |
| `<unit>`       | A unit of time. This can be any of the following: `SECOND`     |
| `<start_date>` | An expression that evaluates to a `DATE` or `TIMESTAMP` value. |
| `<end_date>`   | An expression that evaluates to a `DATE` or `TIMESTAMP` value. |

**Examples**

The example below uses a table `date_test` with the columns and values below.

|          |            |                     |
| -------- | ---------- | ------------------- |
| Category | sale\_date | sale\_datetime      |
| a        | 2012-05-01 | 2017-06-15 09:34:21 |
| b        | 2021-08-30 | 2014-01-15 12:14:46 |
| c        | 1999-12-31 | 1999-09-15 11:33:21 |



```sql
SELECT
	Category,
	DATE_DIFF('YEAR', sale_date, sale_datetime) AS year_difference
FROM
	date_test
```

**Returns**:

```
+----------+-----------------+
| Category | year_difference |
| a        | 5               |
| b        | -7              |
| c        | 0               |
+----------+-----------------+
```

This example below finds the number of days difference between two date strings. The strings first need to be transformed to `TIMESTAMP` type using the `CAST `function.

```sql
SELECT
	DATE_DIFF(
		'day',
		CAST('2020/08/31 10:00:00' AS TIMESTAMP),
		CAST('2020/08/31 11:00:00' AS TIMESTAMP)
	);
```

**Returns**: `0`

## DATE\_FORMAT

Formats a ​`DATE` ​​or ​`DATETIME` ​​according to the given format expression.

**Syntax**

```sql
​​DATE_FORMAT(<date>, '<format>')​​
```

| Parameter  | Description                                                                                                                                                                                |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `<date>`   | The date to be formatted.                                                                                                                                                                  |
| `<format>` | The format to be used for the output using the syntax shown. The reference table below lists allowed expressions and provides example output of each expression for a given date and time. |



| Expression for \<format> | Description                                                                 | Expression output for Tuesday the 2nd of April, 1975 at 12:24:48:13 past midnight          |
| ------------------------ | --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| `%C`                     | The year divided by 100 and truncated to integer (00-99)                    | `19`                                                                                       |
| `%d`                     | Day of the month, zero-padded (01-31)                                       | `02`                                                                                       |
| `%D`                     | Short MM/DD/YY date, equivalent to %m/%d/%y                                 | `04/02/75`                                                                                 |
| `%e`                     | Day of the month, space-padded ( 1-31)                                      | `2`                                                                                        |
| `%F`                     | Short YYYY-MM-DD date, equivalent to %Y-%m-%d                               | `1975-04-02`                                                                               |
| `%H`                     | The hour in 24h format (00-23)                                              | `00`                                                                                       |
| `%I`                     | The hour in 12h format (01-12)                                              | `12`                                                                                       |
| `%j`                     | Day of the year (001-366)                                                   | `112`                                                                                      |
| `%m`                     | Month as a decimal number (01-12)                                           | `04`                                                                                       |
| `%M`                     | Minute (00-59)                                                              | `24`                                                                                       |
| `%n`                     | New-line character (‘’) in order to add a new line in the converted format. | <p>For example, <code>%Y%n%m</code> returns<br><code>1975</code></p><p><code>04</code></p> |
| `%p`                     | AM or PM designation                                                        | `PM`                                                                                       |
| `%R`                     | 24-hour HH:MM time, equivalent to %H:%M                                     | `00:24`                                                                                    |
| `%S`                     | The second (00-59)                                                          | `48`                                                                                       |
| `%T`                     | ISO 8601 time format (HH:MM:SS), equivalent to %H:%M:%S                     | `00:24:48`                                                                                 |
| `%u`                     | ISO 8601 weekday as number with Monday as 1 (1-7)                           | `2`                                                                                        |
| `%V`                     | ISO 8601 week number (01-53)                                                | `17`                                                                                       |
| `%w`                     | weekday as a decimal number with Sunday as 0 (0-6)                          | `2`                                                                                        |
| `%y`                     | Year, last two digits (00-99)                                               | `75`                                                                                       |
| `%Y`                     | Year                                                                        | `1975`                                                                                     |
| `%%`                     | Escape character to use a `%` sign                                          | `%`                                                                                        |

**Example**

The examples below use a table `date_test` with the columns and values below. The following examples use these `TIMESTAMP` values to demonstrate the various `DATE_FORMAT` expressions.

| Category | sale\_datetime      |
| -------- | ------------------- |
| a        | 2017-06-15 09:34:21 |
| b        | 2014-01-15 12:14:46 |
| c        | 1999-09-15 11:33:21 |

The example below shows output for `<format>` expressions %C, %d, %D, %e, %F, %H, %I

```sql
SELECT
	Category,
	DATE_FORMAT(sale_datetime, '%C') AS C,
	DATE_FORMAT(sale_datetime, '%d') AS d,
	DATE_FORMAT(sale_datetime, '%D') AS D,
	DATE_FORMAT(sale_datetime, '%e') AS e,
	DATE_FORMAT(sale_datetime, '%F') AS F,
	DATE_FORMAT(sale_datetime, '%H') AS H,
	DATE_FORMAT(sale_datetime, '%I') AS I
FROM
	date_test
ORDER BY Category
```

**Returns:**

```
+----------+---------------------+----+----+----------+----+------------+----+----+
| Category | sale_datetime       | C  | d  | D        | e  | F          | H  | I  |
| a        | 2017-06-15 09:34:21 | 20 | 15 | 06/15/17 | 15 | 2017-06-15 | 09 | 09 |
| b        | 2014-01-15 12:14:46 | 20 | 15 | 01/15/14 | 15 | 2014-01-15 | 12 | 12 |
| c        | 1999-09-15 11:33:21 | 19 | 15 | 09/15/99 | 15 | 1999-09-15 | 11 | 11 |
+----------+---------------------+----+----+----------+----+------------+----+----+
```

The example below shows output for `<format>` expressions %j, %m, %M, %p, %R, %S

```
SELECT
	Category,
	sale_datetime,
	DATE_FORMAT(sale_datetime, '%j') AS j,
	DATE_FORMAT(sale_datetime, '%m') AS m,
	DATE_FORMAT(sale_datetime, '%M') AS M,
	DATE_FORMAT(sale_datetime, '%p') AS p,
	DATE_FORMAT(sale_datetime, '%R') AS R,
	DATE_FORMAT(sale_datetime, '%S') AS S
FROM
	date_test
ORDER BY Category
```

**Returns:**

```
+----------+---------------------+-----+----+----+----+-------+----+
| Category | sale_datetime       | j   | m  | M  | p  | R     | S  |
| a        | 2017-06-15 09:34:21 | 166 | 06 | 34 | AM | 09:34 | 21 |
| b        | 2014-01-15 12:14:46 | 015 | 01 | 14 | PM | 12:14 | 46 |
| c        | 1999-09-15 11:33:21 | 258 | 09 | 33 | AM | 11:33 | 21 |
+----------+---------------------+-----+----+----+----+-------+----+
```

The example below shows output for `<format>` expressions %T, %u, %V, %w, %y, %Y, %%

```
SELECT
	Category,
	sale_datetime,
	DATE_FORMAT(sale_datetime, '%T') AS T,
	DATE_FORMAT(sale_datetime, '%u') AS u,
	DATE_FORMAT(sale_datetime, '%V') AS V,
	DATE_FORMAT(sale_datetime, '%w') AS w,
	DATE_FORMAT(sale_datetime, '%y') AS y,
	DATE_FORMAT(sale_datetime, '%Y') AS Y,
	DATE_FORMAT(sale_datetime, '%%') AS percent
FROM
	date_test
ORDER BY Category
```

**Returns:**

```
+----------+---------------------+----------+---+----+---+----+------+---------+
| Category | sale_datetime       | T        | u | V  | w | y  | Y    | percent |
| a        | 2017-06-15 09:34:21 | 09:34:21 | 4 | 24 | 4 | 17 | 2017 | %       |
| b        | 2014-01-15 12:14:46 | 12:14:46 | 3 | 03 | 3 | 14 | 2014 | %       |
| c        | 1999-09-15 11:33:21 | 11:33:21 | 3 | 37 | 3 | 99 | 1999 | %       |
+----------+---------------------+----------+---+----+---+----+------+---------+
```

## DATE\_TRUNC

Truncate a given date to a specified position.

**Syntax**

```sql
​​DATE_TRUNC('<precision>', <date>)​​
```

| Parameter     | Description                                                                                           |
| ------------- | ----------------------------------------------------------------------------------------------------- |
| `<precision>` | The time unit for the returned value to be expressed. ​ This can be any of the following: `SECOND`    |
| `<date>`      | The date to be truncated. This can be any expression that evaluates to a `DATE` or `TIMESTAMP` value. |

**Example**

The example below uses a table `date_test` with the columns and values below.

| Category | sale\_datetime      |
| -------- | ------------------- |
| a        | 2017-06-15 09:34:21 |
| b        | 2014-01-15 12:14:46 |
| c        | 1999-09-15 11:33:21 |

```
SELECT
    Category,
    sale_datetime,
    DATE_TRUNC('MINUTE', sale_datetime) AS MINUTE,
    DATE_TRUNC('HOUR', sale_datetime) AS HOUR,
    DATE_TRUNC('DAY', sale_datetime) AS DAY
FROM
	date_test
ORDER BY Category
```

**Returns**:

```
+----------+---------------------+---------------------+---------------------+---------------------+
| Category | sale_datetime       | MINUTE              | HOUR                | DAY                 |
| a        | 2017-06-15 09:34:21 | 2017-06-15 09:34:00 | 2017-06-15 09:00:00 | 2017-06-15 00:00:00 |
| b        | 2014-01-15 12:14:46 | 2014-01-15 12:14:00 | 2014-01-15 12:00:00 | 2014-01-15 00:00:00 |
| c        | 1999-09-15 11:33:21 | 1999-09-15 11:33:00 | 1999-09-15 11:00:00 | 1999-09-15 00:00:00 |
+----------+---------------------+---------------------+---------------------+---------------------+
```

## EXTRACT

Retrieves subfields such as year or hour from date/time values.

**Syntax**

```sql
​​EXTRACT(<field> FROM <source>)​​
```

| Parameter  | Description                                                                                           |
| ---------- | ----------------------------------------------------------------------------------------------------- |
| `<field>`  | Supported fields: `DAY`, `DOW, MONTH`, `WEEK`, `QUARTER`, `YEAR`, `HOUR`, `MINUTE`, `SECOND`, `EPOCH` |
| `<source>` | A value expression of type timestamp.                                                                 |

**Example**

This example below extracts the year from the timestamp. The string date first need to be transformed to `TIMESTAMP` type using the `CAST `function.

```
SELECT
	EXTRACT(
		YEAR
		FROM
			CAST('2020-01-01 10:00:00' AS TIMESTAMP)
	)
```

**Returns**: `2020`

## FROM\_UNIXTIME

Convert Unix time (`LONG` in epoch seconds) to `DATETIME` (YYYY-MM-DD HH:mm:ss).

**Syntax**

```sql
​​FROM_UNIXTIME(<unix_time>)​​
```

| Parameter     | Description                                  |
| ------------- | -------------------------------------------- |
| `<unix_time>` | The UNIX epoch time that is to be converted. |

**Example**

```sql
SELECT 
    FROM_UNIXTIME(1493971667);
```

**Returns**: `2017-05-05 08:07:47`

## NOW

Returns the current date and time.

**Syntax**

```sql
​​NOW()​​
```

**Example**

```
SELECT 
    NOW()
```

**Returns**: `2021-11-04 20:42:54`

## TIMEZONE

Returns the current timezone of the request execution

**Syntax**

```sql
​​TIMEZONE()​​
```

**Example**

```
SELECT 
    TIMEZONE()
```

**Returns**: `Etc/UTC`

## TO\_DAY\_OF\_WEEK

Converts a date or timestamp to a number representing the day of the week (Monday is 1, and Sunday is 7).

**Syntax**

```sql
​​TO_DAY_OF_WEEK(<date>)​​
```

| Parameter | Description                                             |
| --------- | ------------------------------------------------------- |
| `<date>`  | An expression that evaluates to a `DATE `or `TIMESTAMP` |

**Example**

This example below finds the day of week number for April 22, 1975. The string first needs to be transformed to `DATE `type using the `CAST `function.

```sql
SELECT
    TO_DAY_OF_WEEK(CAST('1975/04/22' AS DATE)) as res;
```

**Returns**: `2`

## TO\_DAY\_OF\_YEAR

Converts a date or timestamp to a number containing the number for the day of the year.

**Syntax**

```sql
​​TO_DAY_OF_YEAR(<date>)​​
```

| Parameter | Description                                             |
| --------- | ------------------------------------------------------- |
| `<date>`  | An expression that evaluates to a `DATE `or `TIMESTAMP` |

**Example**

This example below finds the day of the year number for April 22, 1975. The string first needs to be transformed to `DATE `type using the `CAST `function.

```sql
SELECT
    TO_DAY_OF_YEAR(CAST('1975/04/22' AS DATE)) as res;
```

**Returns**: `112`

## TO\_HOUR

Converts a date or timestamp to a number containing the hour.

**Syntax**

```sql
​​TO_HOUR(<timestamp>)​​
```

| Parameter     | Description                                                |
| ------------- | ---------------------------------------------------------- |
| `<timestamp>` | The timestamp to be converted into the number of the hour. |

**Example**

For Tuesday, April 22, 1975 at 12:20:05:

```sql
SELECT TO_HOUR(CAST('1975/04/22 12:20:05' AS TIMESTAMP)) as res;
```

Returns: `12`

## TO\_MINUTE

Converts a timestamp (any date format we support) to a number containing the minute.

**Syntax**

```sql
​​TO_MINUTE(<timestamp>)​​
```

| Parameter     | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| `<timestamp>` | The timestamp to be converted into the number of the minute. |

**Example**

For Tuesday, April 22, 1975 at 12:20:05:

```sql
SELECT TO_MINUTE(CAST('1975/04/22 12:20:05' AS TIMESTAMP)) as res;
```

**Returns:** `20`

## TO\_MONTH

Converts a date or timestamp (any date format we support) to a number containing the month.

**Syntax**

```sql
​​TO_MONTH(<date>)​​
```

| Parameter | Description                                                         |
| --------- | ------------------------------------------------------------------- |
| `<date>`  | The date or timestamp to be converted into the number of the month. |

**Example**

For Tuesday, April 22, 1975:

```sql
SELECT TO_MONTH(CAST('1975/04/22' AS DATE)) as res;
```

**Returns:** 4

## TO\_QUARTER

Converts a date or timestamp (any date format we support) to a number containing the quarter.

**Syntax**

```sql
​​TO_QUARTER(<date>)​​
```

| Parameter | Description                                                           |
| --------- | --------------------------------------------------------------------- |
| `<date>`  | The date or timestamp to be converted into the number of the quarter. |

**Example**

For Tuesday, April 22, 1975:

```sql
SELECT TO_QUARTER(CAST('1975/04/22' AS DATE)) as res;
```

**Returns:**` 2`

## TO\_SECOND

Converts a timestamp (any date format we support) to a number containing the second.

**Syntax**

```sql
​​TO_SECOND(<timestamp>)​​
```

| Parameter     | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| `<timestamp>` | The timestamp to be converted into the number of the second. |

**Example**

For Tuesday, April 22, 1975 at 12:20:05:

```sql
SELECT TO_SECOND(CAST('1975/04/22 12:20:05' AS TIMESTAMP)) as res;
```

**Returns: **`5`

## TO\_STRING

Converts a date into a STRING. The date is any [date data type​​](../../general-reference/data-types.md).

**Syntax**

```sql
TO_STRING(<date>)
```

| Parameter | Description                           |
| --------- | ------------------------------------- |
| `<date>`  | The date to be converted to a string. |

**Example**

This que**r**y returns today's date and the current time.

```sql
SELECT TO_STRING(NOW());
```

**Returns**: ​ `2022-10-10 22:22:33`

## TO\_WEEK

Converts a date or timestamp (any date format we support) to a number containing the week.

**Syntax**

```sql
​​TO_WEEK(<date>)​​
```

| Parameter | Description                                                        |
| --------- | ------------------------------------------------------------------ |
| `<date>`  | The date or timestamp to be converted into the number of the week. |

**Example**

For Tuesday, April 22, 1975:

```sql
SELECT TO_WEEK(CAST('1975/04/22' AS DATE)) as res;
```

**Returns: **`16`

## TO\_YEAR

Converts a date or timestamp (any date format we support) to a number containing the year.

**Syntax**

```sql
​​TO_YEAR(<date>)​​
```

| Parameter | Description                                                        |
| --------- | ------------------------------------------------------------------ |
| `<date>`  | The date or timestamp to be converted into the number of the year. |

**Example**

For Tuesday, April 22, 1975:

```sql
SELECT TO_YEAR(CAST('1975/04/22' AS DATE)) as res;
```

**Returns: **`1975`
