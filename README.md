# THINGS IN HERE

## GEMS

```
gem "sassc-rails"
gem 'haml'
gem 'simple_form'
gem 'devise'
gem 'acts_as_votable'
# gem 'paperclip'
```
- no paperclip needed
- sass rails for .scss files
- image processing for storage
- devise set for turbo, rails 7
- from: https://dev.to/efocoder/how-to-use-devise-with-turbo-in-rails-7-9n9
- haml for devise links

```
#logo= link_to "Muse", root_path
%nav
	- if user_signed_in?
		= link_to current_user.name, edit_user_registration_path
		= link_to "Add New Inspiration", new_post_path, class: "button"
	- else
		= link_to "Sign in", new_user_session_path
		= link_to "Sign Up", new_user_registration_path, class: "button"

```

## MODELS
- devise user: has many posts and comments
- posts: belongs to user
- attached an image
- comments: belong to user, post

## OTHER
- he did his own styling
- added likes and dislikes with acts as votable

```
  resources :posts do
  	member do
  		get "like", to: "posts#upvote"
  		get "dislike", to: "posts#downvote"
  	end
  	resources :comments
	end
  root 'posts#index'
end
```

- had a random post shown in the show page where it isn't the current post
```
	def show
		@comments = Comment.where(post_id: @post)
		@random_post = Post.where.not(id: @post).order("RANDOM()").first

	end
```

- added name filed to devise user

```
  before_filter :configure_permitted_parameters, if: :devise_controller?

	protected

	def configure_permitted_parameters
	  devise_parameter_sanitizer.for(:sign_up) << :name
	  devise_parameter_sanitizer.for(:account_update) << :name
	end
end
```
- added normalize and font awesome via cdn

```
	%link{:rel => "stylesheet", :href => "http://cdnjs.cloudflare.com/ajax/libs/normalize/3.0.1/normalize.min.css"}
	%link{:rel => "stylesheet", :href => "http://maxcdn.bootstrapcdn.com/font-awesome/4.2.0/css/font-awesome.min.css"}
```
