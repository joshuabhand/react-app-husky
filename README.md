This project demonstrates the module Husky. This adds pre-push hooks to our project that are platform independent and standard.

PROS
- All related hooks and scripts can be conveniently described in package.json
- If devs are up-to-date with dependencies, pre-push hooks will run

CONS
- The .huskyrc file needs to be added to the ~ directory which is outside of the project directory
- If devs forget this file, pre-push hook runs every time git push is called

## The Gist of this approach

Git hooks and scripts are described in package.json
```
"husky": {
    "hooks": {
      "pre-push": "npm run lint && npm run test"
	  }
  }
```
The branch deletion exception is contained in .huskyrc
```
#!/bin/sh
grep \(delete\)
if [ $? -eq 0 ]; then
# Do not run tests if deleting remote branch
exit 0
fi
```

## Install Husky

1) "npm install" the new husky module added to package.json
*You may need to run cmd as admin or higher privilege
2) Copy .huskyrc into ~ (Home directory)
3) Test pre-push hooks
	1. git push a valid commit (tests passing)
	
		**lint & tests will run and push will succeed**
	
	2. git push an invalid commit (tests failing)
	
		**lint or tests will run and push will fail**
	
	3. git push to delete a remote branch	
	
		**lint & tests will not run due to exception in .huskyrc**

## More info

https://github.com/typicode/husky/blob/master/DOCS.md
