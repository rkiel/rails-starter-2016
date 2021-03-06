Fire up vagrant

    vagrant up

Connnect to vagrant

    vagrant ssh rails
    cd /vagrant

Create a new rails project

    rm -f Gemfile*
    rails new .

Remove files

    rm README.rdoc

Restore `.gitingore` paths

    echo '/.vagrant'     >> .gitignore
    echo '/.rvmrc'       >> .gitignore
    echo '/node_modules' >> .gitignore

Add new files to git

    git init
    git add .gitignore Gemfile* Rakefile app bin config* db lib log public test vendor
    git add Vagrantfile provision

Commit changes

    git commit -m "rails new"

    cp Gemfile /tmp/Gemfile
    grep -v ^\\s*# /tmp/Gemfile > Gemfile
    
Add a JS runtime

    echo "gem 'therubyracer', platforms: :ruby" >> Gemfile

Install gems

    bundle install --without production

Commit changes

    git add Gemfile*
    git commit -m "added JS runtime"


Start the rails server

    ./bin/rails server -b 192.168.33.10

Vist the the Welcome page

[http://192.168.33.10:3000](http://192.168.33.10:3000)


    cp Gemfile /tmp/Gemfile
    grep -v sqlite3 /tmp/Gemfile > Gemfile

Update Gemfile to be compatable with Heroku

    echo "ruby '2.3.1'"             >> Gemfile
    
    echo "gem 'bcrypt', '~> 3.1.7'" >> Gemfile

    echo "group :development, :test do" >> Gemfile
    echo "  gem 'sqlite3'"              >> Gemfile
    echo "end"                          >> Gemfile

    echo "group :production do" >> Gemfile
    echo "  gem 'pg'"           >> Gemfile
    echo "end"                  >> Gemfile

    echo "group :development do" >> Gemfile
    echo "  gem 'netrc'"         >> Gemfile
    echo "  gem 'rest-client'"   >> Gemfile
    echo "  gem 'heroku-api'"    >> Gemfile
    echo "end"                   >> Gemfile

Update gems

    bundle install --without production

Commit changes

    git add Gemfile*
    git commit -m "make Gemfile compatable with Heroku"
