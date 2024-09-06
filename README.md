# Ruby on Rails Base App & Docker

## Prepare environment, for dev version you can use the example environment:
`cp env-example .env`

## Start the server:
`docker compose up --build`

## Testing It Out
Head [here](http://localhost:8020)

### If initialisation of the database is needed, then run the following commands to initialise the database:
`docker­ compose run drkiq rake db:reset`
`docker­ compose run drkiq rake db:migrate`

### Once our database is initialized, run the following:
`docker compose up`
