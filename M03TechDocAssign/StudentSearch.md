# <div align="center">Implementing a Search By Major and Graduation Date</div>

As a part of the CS3710 Web Applications class, you will need to implement a set of features related to searching for students via the index page. This is targeted at the Employers who will be using this app to search for Job and Internship candidates at the University. 

## **Contents**

1. User Story 4
2. No Search, No Result
3. Search By Major
4. Search By Graduation Date and Relation

## **User Story 4**

```As an employer, I want to be able to search for students to filter based on major and graduation date.```

Acceptance Criteria:

- No students will be displayed until a search is completed
- An option to show all students if chosen
- When searching for student the employer should be able to pick a filter one or both of the following to display students
    - Pick a major
    - Pick “before” or “after" and then pick a date so the search will return all students graduating before or after a certain date on the root webpage.
    - Search results should display: First Name, Last Name, Major, Graduation Date and Actions. In a future iteration you will add a feature to only allow buttons to display for edit and delete when that student is logged in.

## **No Search, No Result**

The following explains how to implement the first two parts of the Acceptance Criteria, not showing any students if there are no search parameters, and showing all students if the user selects to see all students.

Context: At the top of the generated `student_controller.rb` file should be the lines:

    @search_params = params[:search] || {}
    @students = Student.all

These variables are used throughout the index file and make working with the search parameters easier. The first is the list of all parameters from the get request, and the second is a list of references to all students in the database.
Context/

We know that we want no students to be shown if no search parameters are entered when a request is made. There is functionality within Ruby to test if all elements of a list are blank, and we can use this to check if the parameters list is blank, as shown below.

`student_controller.rb`:

    # Thank you to Evan Cline for this code
    if @search_params.values.all?(&:blank?)
      @students = nil
      @no_search_params = true
    end

This removes all elements from the list of references to Students in the database (not the database records themselves), and sets a local variable `no_search_params` to true. This is used later by the View when it is passed no students and must determine whether no students matched the filters or if no filters were entered.

For this design, the View first checks if the `@students` variable is nil (the no data constant in Ruby), and will present a number of students and renders the list of students if there are elements in the list. 
In the case that there are no elements, the user can gain much more clarity if there are separate messages for "No Students were found" and "No Search has been completed".
So, after the rendering of the students in the index file, you will need to check if the `@no_search_params` is true, and add the suffecient HTML to give a message to the user to please enter some search filters. 

## **Search By Major**

In order to present the user with the list of students with a desired major, an employer must be able to select their desired major from a drop down, and press `Search`. Luckily, the Bootstrap frame work makes drop downs quite easy, provided you have a list of the valid majors. Inside the Student Edit/New Form `_form.html.erb`, you should have a dropdown that allows students to select a major from the list of valid majors for the database. (I have this implemented as a list inside the Student Model `app/models/student.rb`.) You can simply paste your version into the `_search_form.html.erb`. Doing so ensures that the functionality of majors students can select for themselves and those employers can search for are consistent and (assuming there are students in the database) will return search results. 

When the request is recieved from the search form, the Contoller's `index` method must filter the list of all students down to only those with the matching major. Searching by student major is quite straight forward thanks to Ruby, and can be done with the .where() method on lists. The below Ruby code checks if the value `:major` is in the list of search parameters, and then reassigns the local variable `@students` to the result of filtering the current list to only those whose field `major:` is equal to the value passed with the search parameter `:major`. 

`student_controller.rb`:


    if @search_params[:major].present?
      @students = @students.where(major: @search_params[:major])
    end

And that is it. Unlike the 'No Search Parameter' feature, no special data is maintained to modify the behavior of the View when searching for specified majors. The View already accounts for if there are no students returned, and there is no real need to specify that the major search specifically found no candidates.

## **Search by Graduation Date and Relation**

A key interest that potential employers have is to know when a student expects to graduate, as this determines what sort of professional relationship the student may be available for. Namely, while a student is in school an internship is often more appropriate that a full-time or even part-time job. In order for an employer who is looking specifically for internship or job candidates specifically to find students who may be a good fit, they need to be able to filter all students in the database down to just those who are graduating before or after a given date. (Note: providing a date range would also be an appropriate/fitting struture but does not strictly meet the requirements).

So, how to implement such a feature. In frankness, I went about it in a slightly strange way. It does function as intended but is not the smoothest experience.

Step 1: Much like the major feature, clone from the Edit Student Form the date picker tag. This is provided by either HTML or Bootstrap and will return a date in the format "yyyy-mm-dd", which will be relevant later. Name the tag according to the graduation date column in your implementation of the database.

Step 2: Inside the `student.rb` file, create a list called something like `Valid_Grad_Relations` containing values that represent before and after. This will be used in a dropdown to allow an employer to indicate if they are looking at candiates graduating before (inclusive) or after(inclusive) some date.

Step 3: Back in the Search Form, immediately before or after the date picker tag, copy the Search by Major tag (you should have two identical tags). First, change the name of the label and the select to something like `graduation_relation` and change the text of the label to "Graduation Relation". (This is to differentiate them from the major search in code.) In the `form.select` tag, change the reference to the list of valid majors to whatever you called your graduation relations list. Finally, change the final element of the `form.select` tag to the identifier of the select and label tags (ex. `graduation_relation`). These changes should create the form changes necessary to let the Controller know what the user is looking for. 

Step 4: (Note: Any undescribed code from the following can easily be created by copying and tweaking code from previous features) In the Controller's `index` method, check if the search parameter `graduation_date` (or whatever your field is called) is present. Then check if the `graduation_relation` search parameter is present. If either one is absent, filtering by graduation is not very meaningful (as searching for a single graduation date is not very helpful given test data). (Note: This is where the graduation relation implementation is perhaps a poor fit) In the case that both are present, separate the date variable using string operations into the four digit year, two digit month, and two digit day into three separate temporary variables. Next compare the `graduation_relation` parameter to the before element of you relation list. In the case that the comparison matches, filter the `@students` list by `graduation_date` on a constructed range from the start of 1970 (the earliest Ruby's time system will allow) to the year, month, and day desired by the user.
A new Ruby Time object can be created with the following:

  Time.new(year_4d, month_2d, day_2d)

The case for after can be created similarly, where the user's date is the start of the range and a date very far into the future is the end. I selected December 31st, 9999. IMPORTANT:: This is a very bad strategy in practice, see [Y2K](https://en.wikipedia.org/wiki/Year_2000_problem), that is of no significance for a test project for a class.

Written by Tyler Andreasen/CanaDev