# Neil's development notes
                                                                                
# Code Smells

Code smells are signs that a refactoring is necessary. It's very important
to get rid of code smell while they are small, because as they increase in your
codebase, they can lead to resistance to change.

# 1 - Bloaters

Bloaters are classes and methods that have increased in size and complexity so  
much that they are really hard to work with. They are those classes that no one
wants to touch and, in general, when someone has to make changes on them to fix
a bug, many other bugs appear.

# 1.1 - Long Method
A method that contains too many lines of code. It's easier to write code than to
read it, as one line of code is written only once and read many times by
different people. A long method that has more than 10 or even 5 lines of code
requires a greater effort to understand and many fragmentss of this method
represent smaller concepts that could have their own methods.

The treatment to long methods is:
- [Exctract Method](#1-extract-method)

If extracting a method is hard, those refactoring techniques could be useful:
- Replace Temp with Query
- Introduce Parameter Object
- Preserve Whole Object


# Refactoring catalog

## 1. Extract Method

Problem: You have a code fragment that can be grouped together:

```ruby
def backup_data
  ObjectStorage.new(generate_user_data_file).save
  
  # Notify by e-mail
  BackupMailer.notify_user(user).deliver_later
  BackupMailer.notify_sysadmin(user).deliver_later
end
```

Solution: Move this fragment to a new method and replace the old code with
a call to this new method.

```ruby
def backup_data
  ObjectStorage.new(generate_user_data_file).save
  
  notify_by_email
end

def notify_by_email
  BackupMailer.notify_user(user).deliver_later
  BackupMailer.notify_sysadmin(user).deliver_later
end


```
