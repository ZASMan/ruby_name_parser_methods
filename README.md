# Basic Ruby Name Parser (Simple String/Array Manipulation Example)

Note: I don't claim that this is a super efficient way to do things, instead I want to share this as a simple example of array/string manipulation in the Ruby Programming language for beginners. For a more comprehensive tool, I suggest a gem such as (Namae)[https://github.com/berkmancenter/namae].

This had a specific use case in which I had a CSV spreadsheet of several hundredvalues where every name was a value in the format of `Last, First Middle` or even `Last, First Middle1 Middle2`. To match up with my data model structure, I needed to extract a first, middle, and last name.
After using Ruby's CSV class to pull the raw name data, I used the following simple methods to extract the names.

Note: the `user_full_name` variable comes from the value pulled from the CSV file.
```
def set_first_name(user_full_name)
  unless user_full_name.nil?
    # This compensates for a format such as
    # Anderson Wayne, Bruce Tom
    # and assumes that Bruce is
    # the first name
    full_name_split_comma = user_full_name.split(',', 0)
    first_and_middle_name = full_name_split_comma[1]
    first_and_middle_name = first_and_middle_name.split(" ")
    first_name = first_and_middle_name[0]
  end
end

def set_last_name(user_full_name)
  unless user_full_name.nil?
    # Split by ',' because , will always come after last name
    user_full_name.strip.split(",")[0]
  end
end

def set_middle_name(user_full_name)
  unless user_full_name.nil?
    names_array = user_full_name.strip.split(",")
    # If there's no middle name, stop here
    # It will be equal to 1 if just 'Wayne, Bruce'
    if names_array[1].split(" ").length == 1
      ""
    else
      # This compensates for case of a name such as
      # Anderson Wayne, Bruce Tom James
      # in the case that "Tom" and "James" are both
      # the middle name to keep both as "Tom James"
      first_and_middle = names_array[1]
      first_and_middle_array = first_and_middle.split(" ")
      first_and_middle_array.delete(first_and_middle_array[0])
      first_and_middle_array.join(" ")
    end
  end
end
```
