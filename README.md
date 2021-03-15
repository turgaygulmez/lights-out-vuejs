# Overview

Lights Out game created by using Vue.js

# Description

This project was bootstrapped with [Vue crate CLI](https://cli.vuejs.org/guide/creating-a-project.html). LightHouseBoard component contains all the implementation to create the lights out game. The component accepts following parameters

| Parameter   | Type        | Description |
| ----------- | ----------- | ----------- |
| lightOnCount      | Number       | Number of cells will be generated randomly
| size   | Number        | Size of the 2d dimensional array

In order to create lights out game. First we initialize 2d array of objects. Each object contains the x and y coordinate of the cell as well as the current state (lightOn). 

Depending on the lightOnCount, we set the light on for some of the cells randonly.

Upon user click, we determine the clicked cell coordinate as first thing. Then the select cell is toggled as either light on or off depending on the state in the 2d array.

We also need to toggle the four adjacent lights which are left, right, top and buttom lights of the selected cell.

In order to find out which lights to toggle. We will use array indexes. Since 

```javascript

      const directions = [
        [1, 0],
        [-1, 0],
        [0, 1],
        [0, -1],
      ];
```

summing x and y coordinate (outter and inner idexes of the array) with above directions will give us the four adjacent lights.

We also need to handle adjacent lights which are out of the array bound. Therefore before adjacent lights are toggled, we need to check whether they are in the array range or not.

Last but not least. Enjoy the game :)

## Enviroment and requirements

- Install [NodeJS version 13+](https://nodejs.org/en/) 
- For better and clean code experience enable VS Code [Vtur extension](https://marketplace.visualstudio.com/items?itemName=octref.vetur)
- run <code>npm run install</code> to install all dependencies

## Available Scripts

In the project directory, you can run:

### `npm run serve`

Runs the app in the development mode.\
Open [http://localhost:8080/](http://localhost:8080/) to view it in the browser.
The page will reload if you make edits.\

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles all files for production mode and optimizes the build for the best performance.