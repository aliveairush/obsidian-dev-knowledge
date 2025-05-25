Introduces in v18 , made default in v19.

It is used for [[hydration]] limitaions.

## Previous problem and solution
1. Static html downloaded by [[Angular server-side rendering]]
2. User clicks button but nothing happens (event not executed)
3. Angular js hydrated html

And the solution 
1. Static html downloaded by [[Angular server-side rendering]]
2. User clicks button but nothing happens
3. Event is dispatched and stored 
4. Angular js hydrated html
5. Event is executed
