# Flash Messages

<%= partial("docs/disclaimer.html") %>

<%= title("What are Flash Messages?", {name:"what-is-flash"}) %>

Flash messages are a means of communicating messages to the end user from inside of an application. These messages might be errors, warnings, or success types of messages.

Some examples of flash messages are:

* "You have been successfully logged out."
* "Your widget could not be updated."
* "There was a problem accessing your account."

Being able to set these messages in a Buffalo handler and then pass them down to views is incredibly helpful.

<%= title("Setting Flash Messages") %>

Creating flash messages can easily be done by using the `c.Flash()` function provided on the [`buffalo.Context`](/docs/context).

<%= code("go") { %>
func WidgetsCreate(c buffalo.Context) error {
  // do some work
	c.Flash().Add("success", "Widget was successfully created!")
  // do more work and return
}
<% } %>

The names of the "keys", in this example, "success", are left up to your application to use as is appropriate. There are no "special" or "pre-defined" keys.

<%= title("Accessing Flash Messages in Templates", {name: "accessing-in-templates"}) %>

### Looping Over all Flash Messages

<%= code("html") { %>
<div class="row">
  <div class="col-md-12">
    \\<%= for (k, messages) in flash { %>
      \\<%= for (msg) in messages { %>
        &lt;div class="alert alert-\\<%= k %>" role="alert">
          &lt;button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button>
          \\<%= msg %>
        </div>
      \\<% } %>
    \\<% } %>
  </div>
</div>
<% } %>

### Looping Over a Specific Flash Message Key

<%= code("html") { %>
<div class="row">
  <div class="col-md-12">
    \\<%= for (message) in flash["success"] { %>
      &lt;div class="alert alert-success" role="alert">
        &lt;button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        \\<%= message %>
      </div>
    \\<% } %>
  </div>
</div>
<% } %>