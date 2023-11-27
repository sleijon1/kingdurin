# kingdurin

I have mostly been working with Flask and uWSGI in my Python web adventures which has meant synchronous parallel processing. I recently discovered FastAPI and found it a very interesting choice since it has some benefits over Flask and other Python web frameworks such as Django.

So in this project my aim is to test out the asyncness of FastAPI. 

([Fun conversations on ASGI vs uWSGI](https://www.reddit.com/r/flask/comments/xvw1vi/misunderstandings_about_how_async_works_with/))

## Main idea

Launch two applications running FastAPI.

The first application will be where the async action happens. This application will make calls to the the second application and
the second application is going to be CPU heavy while the first application will be IO heavy because of the CPU heaviness of the second application.

The first application will have single route `/dig` which will cause it to `await` a `/dig` request to the second application. In the second application
each `/dig` request will start the slow process of mining Mithril from the deep dwarven caves, clearly a intense time-consuming activity. 

The expected result is obvious: We should be able to post countless `/dig` requests to the first application and see them all processed while
the second application will be stuck at how many processes we are running the API with.

