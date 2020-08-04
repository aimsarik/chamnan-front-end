# chamnan
<h2>complete core-banking solution and platform for business management</h2>
Note
Chamnan folder: root (Master Project)
    config: Django project
    frontweb: react project 
<h3> Create Django Project Install </h3>
<p>  - Set up Virtual Environment and install Django with other dependencies and libraries later</p>
<p>  - Create django project with name 'config'</p>
<p>     $ django-admin startproject config . </p>
<h3> Create React App </h3>
<p>  - Install create-react-app system-wide</p>
<p>     $ npm install -g create-react-app</p>
<p>  - Create React app with name 'frontweb', eject the config files so that we can edit them and run test it</p>
<p>     $ create-react-app frontweb</p>
<p>     $ cd frontweb</p>
<p>   <del>$ npm run eject</del></p>
<p>     $ npm run start</p>

    - Created backend folder at project root to house all django apps, templates
    - Added path of backend/templates in TEMPLATES in config.settings
