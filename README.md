This project demonstrates the module Husky.

PROS
- All related hooks and scripts can be conveniently described in package.json

CONS
- The .huskyrc file needs to be added to the ~ directory which is outside of the project directory.

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
2) Copy .huskyrc file into ~ (Home directory; usually something like C:/Users/<profile_name>)

There should be few problems if any during installation and usage.
I'm preferring this module over pre-push.

## More info

https://github.com/typicode/husky/blob/master/DOCS.md
