---
layout: post
title:      "Rails Scopes"
date:       2019-12-27 17:23:22 -0500
permalink:  rails_scope_method
---


One feature of Rails are [scopes](https://guides.rubyonrails.org/active_record_querying.html#scopes) for models as a way to return specific objects that meet certain criteria. It uses the ActiveRecord query interface so raw SQL statements are not written. Class methods can also be used, but one difference is that a class method can cause a `NoMethodError `if it is chained with other methods and a conditional evaluate to false. A scope will always return an `ActiveRecord::Relation` object.

Here is an example of a scope that returns a list of objects that all have a specific category. The category is a string that is passed in when the named scope method is called. Each part is explained below.

```
class Emission < ApplicationRecord
  belongs_to :food
  belongs_to :student

  validates :unit, :presence => true
  validates :amount, :presence => true
  validates :source, :presence => true

  scope :category, -> (category) {where("food.category LIKE ?", category)}
	
end

```

`scope` is the method used in the class to define the scope. There can be multiple scopes in a class.

`:category` is the name of this scope.

`(category)` is the argument being passed in. In this example it is a string.

`where` is applying a condition to limit the objects returned. It represents the `WHERE` part of a SQL query.

`food.category` is the field where the condition is applied.  In this example, the field is on an associated model, food.

`?` The question mark will be replaced by the `category`. This syntax is used to avoide the less secure `food.category LIKE category`.

While explaining each part of this scope I came across some examples that use `LIKE` and others that use `=`.  I plan to research these two options to see if they produce different results and if there is a difference in security between the two.
 



