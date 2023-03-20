# Tradeful test

## Overview

To install app: 

1. clone repo
2. run `composer install `
3. run `./vendor/bin/sail up`
4. run `./vendor/bin/sail composer install`
5. run `./vendor/bin/sail artisan migrate --seed`
6. run `./vendor/bin/sail npm install && ./vendor/bin/sail npm run dev`
7. open browser to `localhost:85` (or whichever port you configured in the .env file)
