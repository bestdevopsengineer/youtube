<img width="798" height="458" alt="image" src="https://github.com/user-attachments/assets/d572ba17-d639-48b0-8148-70469c0d403f" />

# design patterns
<img width="1013" height="507" alt="image" src="https://github.com/user-attachments/assets/73c5f7ea-85d2-4f97-a0d4-d7bb98fb1ed8" />

          1-co-located containers
             2 services depends of each other
             there is not an order to which start first
          2- regular init container
            check database to get ready before start the main application
            init starts and stop
          3- sidecar containers
            like init, sidecar starts first and doesnt stop
            main app start after it 
            stop after the main app stops
            
