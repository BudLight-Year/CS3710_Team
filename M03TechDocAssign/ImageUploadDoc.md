# Setting Up Image Upload and Profile Picture Functionality in Rails

## Table of Contents
1. Introduction
2. Setup Active Storage
3. Updating the Student Model
4. Displaying a Default Profile Picture
5. Resources

## Introduction

Active Storage is a convenient tool in Rails that handles file uploads, connecting them to Active Record models that store their information. This guide will explain how to set up Rails' Active Storage to upload images using a student model. Additionally, this guide will explain how to set up a profile picture for a student’s profile page.

## Setting Up Active Storage

1. **Install Active Storage**: Run `rails active_storage:install` to install Active Storage. This will set up the configuration files and migrations for our next step.

2. **Migrate Active Storage**: Run `rails db:migrate` to create the Active Storage tables from the migrations created when Active Storage was installed. These tables will store the information about uploaded images.

## Updating the Student Model to Have and Display a Profile Picture

1. **Update Model to Have One-to-One Relationship with Profile Picture**: First, inform Rails that each student will have only one profile picture. Navigate to the Ruby file for the student model at `app/models/student.rb`. Inside, add the relationship:

    ```ruby
    class Student < ApplicationRecord
      has_one_attached :profile_picture
    end
    ```

    `has_one_attached` is a method provided by Active Storage that associates a model with one file, in our case the file is referred to as `profile_picture`.
    Note: Use `has_many_attached` if you want the model to have many photos.

2. **Update Form to Allow Image Upload**: Now, navigate to the view for the student’s form at `app/views/students/_form.html.erb`. Inside the view, add the field to upload the profile picture:

    ```erb
    <%= form.label :profile_picture %>
    <%= form.file_field :profile_picture %>
    ```

3. **Display Image in Detailed View of Student**: Next, navigate to the detailed view for the student at `app/views/students/show.html.erb`. Inside the view, add:

    ```erb
    <p>
      <strong>Profile Picture:</strong>
      <% if @student.profile_picture.attached? %>
        <%= image_tag @student.profile_picture, size: "300x300" %>
      <% else %>
        No profile picture uploaded.
      <% end %>
    </p>
    ```

    Above, we check if the student has a profile picture attached to its entity in the database. If it does, we display the image, passing a size argument resizing the picture to 300x300 pixels.

4. **Update Parameters in Student Controller**: Finally, we have to update the parameters in the Student controller:

    ```ruby
    def student_params
      params.require(:student).permit(:profile_picture)
    end
    ```

    This will permit the `profile_picture` to be attached and saved to the student model.

## Displaying a Default Profile Picture

1. **Place Default Profile Picture Image in Assets Directory**: A default profile picture is a placeholder image to be displayed when the user has not yet uploaded their own profile picture. To display a default profile picture, you first have to store the image in your application. Simply upload a default profile picture image inside the `app/assets/images` directory with a recognizable name such as `default_profile.png`.

2. **Update Detailed View to Display Default Profile Picture**: Back in the student's detailed view at `app/views/students/show.html.erb`, update the code that you implemented earlier:

    ```erb
    <p>
      <strong>Profile Picture:</strong>
      <% if @student.profile_picture.attached? %>
        <%= image_tag @student.profile_picture, size: "300x300" %>
      <% else %>
        <%= image_tag 'default_profile.png', size: "300x300" %>
      <% end %>
    </p>
    ```

    In the code above, the `default_profile.png` is displayed when the student model has no `profile_picture` attached to it. Once again, the size is modified to ensure consistency in image size. Since the image was placed in the images of the assets folder, Rails will automatically know how to find it when we specify its tag.

## Conclusion

Congratulations, you have successfully set up and migrated Active Storage, updated the student model and parameters to connect the model to an image, updated the form to allow image upload, and updated the view to display the image or default image. This process can be applied to any model for any image upload functionality.

## Resources

- Active Storage Overview — Ruby on Rails Guides: https://edgeguides.rubyonrails.org/active_storage_overview.html
- ActiveStorage (rubyonrails.org): https://rubyonrails.org/
- Ruby on Rails Guides: https://guides.rubyonrails.org/
