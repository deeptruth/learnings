
# Prototype Database Style #

### Things to be consider: ###
1. Folder Structure.
2. Configuration or Convention.
3. Scope of the Data Structure to the any types of system.
4. Security.
5. Time and Space Complexity.
6. Modularity
    - meaning all the module is not tightly coupled you need to analyze carefully the module
    to make it independent.
7. Flowchart Example how to install a module.
8. "Plugin" consider as a abstract layer that will not dependent in the model of the application.

#### Note: #####
1. Hooks.
    - install
    - uninstall
2. Need to present a way of saving a data in a flexible data structure.

#### Question: ####
1. How will the proposed data structure cater the flexibility.

## Drupal
- They're using Entity
- Problem:
    - Joining Tables
    - Distinct

## Wordpress
- They're allowed the developer to build own schema and optional to apply the prefix for each table
that are set in the wp-config.php

##### Proposed Data Structure: #####

Benefits of EAV:
1. Can easily add new column without altering the whole table.
2. Eliminate the null column in each row.