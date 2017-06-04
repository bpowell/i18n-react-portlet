# React Portlet

An old portlet with a new face!

## Getting Started
1.  Javascript framework used: [React framework](https://facebook.github.io/react/)
2.  Tool to build our javascript application: [Yarn](https://yarnpkg.com/en/)
3.  UI library used: [Material UI](http://www.material-ui.com/#/)
4.  i18n support: [react-i8next](https://github.com/i18next/react-i18next)
5.  [i18next](https://www.i18next.com/)

Yarn does not have to be installed locally on your system to build the application. Yarn and node will be downloaded and installed via the maven build process. This is all handled by the frontend maven plugin.

### Prerequisites
1.  maven 3+
2.  jdk 7+ (preferably 8)

## Installing
```bash
mvn clean package
cd $UPORTAL_SOURCE
ant deployPortletApp -DportletApp=/path/to/portlet.war
```

## i18n
The starting point of adding in i18n support in react is in this file [i18n.js](src/main/react/src/i18n.js). 

```javascript
backend: {
    loadPath: "/reactportlet/js/locales/{{lng}}/{{ns}}.json"
},
```

This tells the program where to load the i18n text from. If you had tomcat running on port 8080, you could see the 'en' language with the view namespace will be viewable on http://localhost:8080/reactportlet/js/locales/en/view.json. You can change the location of where the json is to serve up translations.

The react [index.js](src/main/react/src/index.js) file needs to be updated too. You have to wrap the main component with the component `I18nextProvider`.

In all components that will have translations, you have to change how they are exported. It should look something like: `export default translate("view", { wait: true })(App)`

The translations live in the [js](src/main/webapp/js/) folder based on locale. Since we only have one [namespace](https://www.i18next.com/principles/namespaces.html), we just have a view.json file in each folder.

## Building the project.
You do not need to build the react side of the project by its self. The maven process will build and copy the generated artifacts to the correct location for you. But if you wish to build the react project by hand, go to the src/main/react/ directory and do either a `npm run build` or a `yarn run build`.
