# rails-module-polymorphic-assoc
> Rails polymorphic associations example.


## step by step:
+ create model
```bash
rails g model Comment content:text commentable_id:integer commentable_type
rails g model Article title:string content:text
rails g model Photo title:string url:string

rake db:migrate
```
+ create associations:
```rb
# model/comment.rb
class Comment < ApplicationRecord
    belongs_to :commentable, :polymorphic => true
end

# model/article.rb
class Article < ApplicationRecord
    has_many :comments, :as => :commentable
end

# model/photo.rb
class Photo < ApplicationRecord
    has_many :comments, :as => :commentable
end
```

## something important:
### equal model:
```conf
PART-A === PART-B

PART-A
t.integer :commentable_id
t.string :commentable_type

PART-B
t.belongs_to :commentable, :polymorphic => true
```
### code:
```rb
class CreateComments < ActiveRecord::Migration[5.1]
  def change
    create_table :comments do |t|
      t.text :content
#      t.integer :commentable_id
#      t.string :commentable_type

       t.belongs_to :commentable, :polymorphic => true

      t.timestamps
    end
  end
end
```