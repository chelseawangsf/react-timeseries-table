# React Timeseries Table

This library contains a `Table` component for rendering [pond.js](http://software.es.net/pond) TimeSeries objects. The library is used on the public facing [ESnet Portal](http://my.es.net).

Getting started
---------------

This library is intended to be installed with [npm](https://www.npmjs.com/) and the built into your project with a tool like [Webpack](https://webpack.github.io/). It expects React to be present, as well as our TimeSeries abstraction library, [pond.js](http://software.es.net/pond). More on this library below.

To install:

    npm install react-timeseries-table pondjs --save

Once installed, you can import the `Table` component from the library:

    import Table from "react-timeseries-table";

Then we construct our table in the `render()` function of our component. For a simple example let's create a table from some network availability data.

The first step is to take our data and construct a new `TimeSeries` object. The pond.js constructor uses a pretty simple format. Just supply a name, the columns and list of points. For the columns, the first column should be either "index" for a string based time range (such as a month, as shown below), or "time", for a timestamp (represented by number of ms since the epoch):

    const availability = new TimeSeries({
        "name": "availability",
        "columns": ["index", "uptime", "notes", "outages"],
        "points": [
            ["2015-06", 100, "", 0],
            ["2015-05", 92, "Router failure June 12", 26],
            ["2015-04", 87, "Planned downtime in April", 82],
            ["2015-03", 99, "Minor outage March 2", 4],
            ...
        ]
    });

Now that we have a TimeSeries made from our data, we need to define what our table will look like. We do this by defining our columns. This maps our data into our table:

    const columns = [
        {key: "time", label: "Timestamp"},
        {key: "uptime", label: "Availability"},
        {key: "outages", label: "Outages", format: "04d"}
    ];

Then we can render our table:

    <Table series={availability} timeFormat="MMMM, YYYY" columns={columns} />

Developing
----------

The repo contains the examples website. This is very helpful in developing new functionality. Within a cloned repo, you first need to run:

    npm install

This will install the development dependencies into your node_modules directory.

You can then start up the test server, as well as automatic source building, by doing:

    npm run start-website

Then, point your browser to:

[http://localhost:8080/webpack-dev-server/](http://localhost:8080/webpack-dev-server/)

License
-------

This code is distributed under a BSD style license, see the LICENSE file for complete information.

Copyright
---------

ESnet's React Timeseries Table, Copyright (c) 2016, The Regents of the University of California, through Lawrence Berkeley National Laboratory (subject to receipt of any required approvals from the U.S. Dept. of Energy). All rights reserved.

If you have questions about your rights to use or distribute this software, please contact Berkeley Lab's Technology Transfer Department at TTD@lbl.gov.

NOTICE. This software is owned by the U.S. Department of Energy. As such, the U.S. Government has been granted for itself and others acting on its behalf a paid-up, nonexclusive, irrevocable, worldwide license in the Software to reproduce, prepare derivative works, and perform publicly and display publicly. Beginning five (5) years after the date permission to assert copyright is obtained from the U.S. Department of Energy, and subject to any subsequent five (5) year renewals, the U.S. Government is granted for itself and others acting on its behalf a paid-up, nonexclusive, irrevocable, worldwide license in the Software to reproduce, prepare derivative works, distribute copies to the public, perform publicly and display publicly, and to permit others to do so.
