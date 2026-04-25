## Overview

This page documents main parameter in the 4D_Info_Report reference.

## Description of the main parameter for the creation of reports

(For all shared methods that create a report, most often the second (optional) parameter).

- **ContentMode Value** (var type: integer) — Define the mode of the description of report (for tables):

| Main parameter value<br>for the creation of reports: | -2 | -1 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Count total number of records… | X | X | X | X | X | X | X | X | X | X | X | X |
| except for invisible tables | X |   |   |   | X | X | X | X | X |   |   |   |
| Hide Table List | X | X |   |   |   |   |   |   |   |   |   |   |
| (Default if parameter omitted) Show all tables list, with all structure details |   |   | X |   |   |   |   |   |   |   |   |   |
| Show Table List: |   |   | X | X | X | X | X | X | X | X | X | X |
| Show Table Number |   |   | X | X | X | X | X | X | X | X | X | X |
| Show Table Name |   |   | X | X | X | X | X | X | X | X | X | X |
| Show number of records of the table |   |   | X | X | X | X | X | X | X | X | X | X |
| Show number of indexed fields |   |   | X |   |  | X | X | X | X | X | X | X |
| Show number of subtable (if any) |   |   | X |   |   | X |   | X |  |   | X |   |
| Show triggers |   |  | X |   |   | X | X |   |   | X |   |   |

(For all shared methods that create a report, most often the last (optional) parameter).

- **Nb processes list** (Var type: integer) — Define the number of processes to list in the report

(Pass the value -1 to list all the (alive) processes running on 4D / 4D Server.)

<!-- NAV_BUTTONS_START -->
## Navigation

[Previous](./03_list_of_shared_methods.md) | [Summary](./01_introduction.md) | [Next](./05_standalone.md)
<!-- NAV_BUTTONS_END -->
