# RSpec Testing Documentation

## Table of Contents
1. Setup
2. Making a Test Group
3. Setting Up More Specific Test Groups
4. Setting Up Context Test Groups
5. Creating Data for the Test Database
6. Setting Up Specific Tests
7. Tests and Assertions

---

## Setup

1. **Install RSpec Rails**: In your Rails `Gemfile`, under the `:development, :test` group block, add the following gem:

    ```ruby
    gem 'rspec-rails', '~> 6.0'
    ```

2. **Install the Gem**: Run the following in your terminal:

    ```bash
    bundle install
    ```

3. **Generate RSpec Files**: Run this command to generate the necessary RSpec files:

    ```bash
    rails generate rspec:install
    ```

4. **Generate a Test File**: To generate a test file for your model, run:

    ```bash
    rails generate rspec:request student
    ```

    Replace `student` with the name of the model you are testing.

---

## Making a Test Group

To begin writing tests, create a test group using `RSpec.describe`, followed by the name of the test group and the type of test. For example:

```ruby
RSpec.describe "Students", type: :request do
end
```

This example sets up a request test group. For more test group types, refer to the [RSpec Documentation](https://rspec.info/).

---

## Setting Up More Specific Test Groups

Each method that needs to be tested should have its own test group. Use the `describe` keyword to create a new method group.

Example:

```ruby
RSpec.describe "Students", type: :request do
  describe "GET /students" do
  end
end
```

In this example, a method test group for `GET /students` is created.

---

## Setting Up Context Test Groups

To create a test group for specific conditions, use the `context` keyword followed by a name describing the condition.

Example:

```ruby
RSpec.describe "Students", type: :request do
  describe "GET /students" do
    context "when students exist" do
    end
    context "when no students exist" do
    end
  end
end
```

Here, two context groups are created: one for when students exist and another for when no students exist.

---

## Creating Data for the Test Database

Within each context group, use the `let!` keyword to create data that will be executed before the test starts.

Example:

```ruby
RSpec.describe "Students", type: :request do
  describe "GET /students" do
    context "when students exist" do
      let!(:student) { Student.create!(first_name: "Aaron", last_name: "Gordon") }
    end
    context "when no students exist" do
    end
  end
end
```

In this example, a student is created in the database before each test inside the "when students exist" group.

---

## Setting Up Specific Tests

Once your groups and dummy data are ready, define individual test cases using the `it` keyword.

Example:

```ruby
RSpec.describe "Students", type: :request do
  describe "GET /students" do
    context "when students exist" do
      let!(:student) { Student.create!(first_name: "Aaron", last_name: "Gordon") }

      it "returns a successful response and displays the search form" do
      end
    end
    context "when no students exist" do
      it "displays a message prompting to search" do
      end
    end
  end
end
```

Each test case is defined within its respective context group.

---

## Tests and Assertions

Finally, insert statements and assertions using the `expect` keyword to verify test outcomes.

Example:

```ruby
RSpec.describe "Students", type: :request do
  describe "GET /students" do
    context "when students exist" do
      let!(:student) { Student.create!(first_name: "Aaron", last_name: "Gordon") }

      it "returns a successful response and displays the search form" do
        get students_path
        expect(response).to have_http_status(:ok)
        expect(response.body).to include('Search')
      end
    end

    context "when no students exist" do
      it "displays a message prompting to search" do
        get students_path
        expect(response.body).to include("Please enter search criteria to find students")
      end
    end
  end
end
```

In each test case, an `expect` statement checks the result of the request to ensure the expected outcome.
