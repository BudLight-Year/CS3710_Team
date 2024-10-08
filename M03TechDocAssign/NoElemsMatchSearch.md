# Documentation for No Search Results Message

After implementing the Search By Major Feature, I found that if I selected a major that had no associated students, the page would show the New Student option immediately below the Search menu, which does not look very good.
After a bit of thought as to how I might go about this, I implemented the following Embedded Ruby in the `index.hml.erb` file:

```
<% if @students.count > 0 %>
    <% @students.each do |student| %>
        <%= render student %>
        <p>
            <%= link_to "Show this student", student %>
        </p>
    <% end %>
<% else %>
    <p> No matching students were found. </p>
<% end %>
```

This, built on code supplied to render all students, will render any students if the search returns one or more students, but will display a clear message to the user that the search operation completed but yielded no results.