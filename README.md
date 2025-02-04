# Simply get together
### CHECK DEPLOYED <img src="https://img.shields.io/badge/Heroku-430098?style=for-the-badge&logo=heroku&logoColor=white"> APP [HERE](https://akord-app.herokuapp.com/)
You don't find the way to agree with your friends for your events or to go out. We have the solution, in Akord you can create an event to go anywhere, you only need sign in and create an event for you and your friends, even your family. Choosing the date for a special ocassion is now easier with the help of Akord.

<p align="center">
<a  target="_blank" href="https://akord-app.herokuapp.com/"><img src="https://user-images.githubusercontent.com/71459774/160011831-cadb6eac-4eb8-4265-b981-a7c00a7fb6a5.png"></a>
</p>

<p align="center">
<a  target="_blank" href="https://akord-app.herokuapp.com/"><img src="https://user-images.githubusercontent.com/72522628/160181073-66255ceb-f8d2-4994-9cf8-a0f0c9884357.png"></a>
</p>

## Main APP Features
- A usear can Sing up and Log in the app to create a new event.
<p align="center">
<a  target="_blank" href="https://akord-app.herokuapp.com/"><img src="https://user-images.githubusercontent.com/71459774/160005074-400d9022-9085-45bb-bf40-4584bc160d99.png"></a>
</p>

<p align="center">
<a  target="_blank" href="https://akord-app.herokuapp.com/"><img src="https://user-images.githubusercontent.com/71459774/160004990-901a42b1-10bb-46c0-a9a4-e20b9d1e97f8.png"></a>
</p>

- A user can create an Event!
<p align="center">
<a  target="_blank" href="https://akord-app.herokuapp.com/"><img src="https://user-images.githubusercontent.com/72522628/160189762-0a65b86b-d7cb-4f44-8f52-cf4b1fcc4eaf.png"></a>
</p>

- A user can't select past dates when creating an event
```ruby
  validate :votable_date_before_today
  def votable_dates
    votable_dates_strings.map { |ds| ::Date.parse(ds) }
  end

  private

  def votable_date_before_today
    errors.add(:votable_dates_strings, "Cannot select past dates") if any_past_dates?
  end

  def any_past_dates?
    votable_dates.any? { |date| date < ::Date.current }
  end
```
- A user can share the event
<p align="center">
<a  target="_blank" href="https://akord-app.herokuapp.com/"><img src="https://user-images.githubusercontent.com/72522628/160190469-14e5d0ed-e66a-4954-9ca0-8a73cfdbde30.png"></a>
</p>

```ruby
<% if current_user&.owns?(@event) %>
      <div data-controller="clipboard" data-clipboard-feedback-text-value="Copied!">
        <input value="<%= short_join_event_url(@event.funid) %>" data-clipboard-target="input" type="text" readonly>
        <button class="btn btn-primary" data-action="click->clipboard#copy">Share with your compas</button>
      </div>
    <%end%>
```
```JavaScript
import { Controller } from "stimulus";

export default class extends Controller {
  static targets = ["input"];
  static values = {
    feedbackText: String
  }

  copy(event) {
    this.inputTarget.select();
    document.execCommand('copy');
    event.currentTarget.disabled = true;
    event.currentTarget.innerText = this.feedbackTextValue;
  }
}

```
- Attendees can join and VOTE for an event!
<p align="center">
<a  target="_blank" href="https://akord-app.herokuapp.com/"><img src="https://user-images.githubusercontent.com/71459774/160006498-20e7a29f-158a-41d5-8eeb-485f1417dbbc.png"></a>
</p>

- Attendees can vote for different dates for the event in an interactive way (Using Hammer.js for swiping animations)
![image](https://user-images.githubusercontent.com/71459774/160006947-14b9d064-ba25-4f60-89fe-35fd74de963c.png)

- Attendess can see a the "Live Voting" for the selected DATES!
<p align="center">
<a  target="_blank" href="https://akord-app.herokuapp.com/"><img src="https://user-images.githubusercontent.com/72522628/160191709-434d849c-2fce-43a2-9544-34738623435d.png"></a>
</p>

- The event creator can select a winning date based on results, so that everyone can see it on their phones and even add it to their preffered calendar!
<p align="center">
<a  target="_blank" href="https://akord-app.herokuapp.com/"><img src="https://user-images.githubusercontent.com/72522628/160192203-1923108b-20d1-4c5f-8fbd-469380bf76de.png"></a>
</p>
<p align="center">
<a  target="_blank" href="https://akord-app.herokuapp.com/"><img src="https://user-images.githubusercontent.com/72522628/160192238-13fed36d-059b-4cd4-a325-f53d61bcd276.png"></a>
</p>

<h1 align="center">
Please feel free to check the APP and experiment yourself!!!👻
</h1>

> [AKORD.ME🗓️ https://www.akord.me/](https://akord-app.herokuapp.com/)

## APP DB SCHEMA
![image](https://user-images.githubusercontent.com/72522628/158682746-1f6e0c6d-0b9d-4e76-bf93-7a9aadbad80f.png)


## Things you may want to cover to initialize this project:
### Versions
> <img src="https://img.shields.io/badge/Ruby-CC342D?style=for-the-badge&logo=ruby&logoColor=white"> <strong> 3.0.3p157 (2021-11-24 revision 3fb7d2cadc) [x86_64-linux]</strong><br>
> <img src="https://img.shields.io/badge/Ruby_on_Rails-CC0000?style=for-the-badge&logo=ruby-on-rails&logoColor=white"> <strong> 6.1.4.6 </strong>
### Tools Used
> Active Record (Example: `rails g model`) <br>
> Heroku Deployment `heroku/7.59.2 linux-x64 node-v12.21.0 `<br>
> `pgcrypto` (in order to add `:uuid` or <strong>Universally unique identifier</strong> to an attendee, so that a user logged in can also vote) <br>
>  `hashid rails` Instead the event model ID using sequential numbers like 1, 2, 3, it will instead have unique short hashes like "yLA6m0oM" <br>
> <img src="https://user-images.githubusercontent.com/72522628/158295411-9dd5ff4a-e40c-4d15-a0b9-0ec257d5ea6f.png"> <br>
> gem 'devise' <br>
> gem "faker" <br>
> gem "groupdate" <br>
> gem "hashid-rails", "~> 1.0" <br>

<h1 align="center">
Please feel free to check the APP source code👾
</h1>

## Setup

```shell
 git clone git@github.com:daniel-enqz/akord.git
 cd akord
 rails db:create db:migrate db:seed:replant
 bundle install
 yarn install
 rails server
```
Open you browser and visit `localhost:3000`
