---
title: FoodcriticRubocop
layout: default
---

Raw notes... needs formatting, context, examples

    ​gem install chefstyle
    - rubocop or rubocop -r chefstyle -D --format offenses
    foodcritic .
    foodcritic -t -FC002 -f all .
    foodcritic -t correctness
    chef exec rspec
    script:
    - chefstyle
    - foodcritic .
    - chef exec rspec
    - kitchen test -d always
    chefstyle -a
