# Order-Processing-Simulator
Two-level parallel program written in Java that processes orders and products and modifies their shipping status.

Files description:

Tema2:
    main thread: - creates the level 1 threads and runs them, assigning to each one of them
                 a task pool of fixed size (equal to the max number of threads)
                 - in the end, it joins the level 1 threads and shuts down the task pools

LevelOneWorker:
    - takes one line at a time from orders.txt and separates the fields
    - initializes a semaphore to keep the level one worker waiting until all products are
    found and shipped by level two workers
    - resets the file pointer to the beginning of the file (the products of every order
    must be searched through the whole file every time)
    - adds a task to the level two task pool
    - ships order -> writes it in the output file and marks it as 'shipped'

LevelTwoWorker:
    - takes one line at a time from order_products.txt and separates the fields
    - ships product -> writes it in the output file and marks it as 'shipped'
    - if a worker finds a product from the current order it adds a permit to the
    level one worker's semaphore

IOHandler:
    - manages all actions that imply input and output files
