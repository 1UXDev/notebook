# React Project Setup

## Learning Objectives

- Having a general understanding of project scaffolding
- Learning how to work with Create React App
- Knowing the purpose of a bundler
- Understanding common `npm` scripts
- Knowing the difference between `public` and `src` folder

---

## Project Scaffolding

Project scaffolding is the process of creating a new project. You will use the
[Create React App](https://create-react-app.dev/docs/getting-started) tool to create a new React
project automatically.

> 💡 In principle, you could create a new React project from scratch. However, this would be a lot
> of work and we would have to set up a lot of things ourselves. For example, you would have to set
> up a development server, a build process and a test runner. You would also have to configure up a
> module bundler and a transpiler. This is a lot of work and you would have to do it every time you
> want to create a new project.

> 💡 Create React App, by the way, works quite similar to the `ghcd` tool you have probably already
> used.

## Create React App

Create React App is a tool that allows you to create a React project with a single command. It is a
great tool to get started with React.

> 📙 Read
> [**Getting Started** on the Create React App Docs](https://create-react-app.dev/docs/getting-started)
> to learn how to create a new project using `npx`.

### Folder Structure

Create React App scaffolds a folder structure for you with a lot of files and folders.

> 📙 Read more about
> [**Folder Structure** on the Create React App Docs](https://create-react-app.dev/docs/folder-structure).

### Available Scripts

Create React App has a few more npm scripts than the ones you have seen so far. Besides starting a
development server and running tests, you can use them to build your app.

> 💡 You should never need to use the `eject` script. It is a one-way operation that you can't undo.
> It is used to customize the configuration of your app.

> 📙 Read more about
> [**Available Scripts** on the Create React App Docs](https://create-react-app.dev/docs/available-scripts).

### Adding a Stylesheet

You can directly import CSS files in your JavaScript files.

It is a common pattern to colocate your CSS with your components. This means that you have a CSS
file with the same name as the component that is imported in the components JavaScript file. It's a
good practice to use the BEM naming convention for your CSS classes to avoid naming conflicts
between components.

> 📙 Read more about
> [**Adding a Stylesheet** on the Create React App Docs](https://create-react-app.dev/docs/adding-a-stylesheet).

### Adding Images, Fonts and Files

You can directly import image files or fonts in your JavaScript files.

This is especially useful for SVG files, which you can import as React components.

> 📙 Read more about
> [**Adding Images, Fonts and Files** on the Create React App Docs](https://create-react-app.dev/docs/adding-images-fonts-and-files).

## Resources

- [Getting Started on the Create React App Docs](https://create-react-app.dev/docs/getting-started)
- [Folder Structure on the Create React App Docs](https://create-react-app.dev/docs/folder-structure)
- [Available Scripts on the Create React App Docs](https://create-react-app.dev/docs/available-scripts)
- [Adding a Stylesheet on the Create React App Docs](https://create-react-app.dev/docs/adding-a-stylesheet)
- [Adding Images, Fonts and Files on the Create React App Docs](https://create-react-app.dev/docs/adding-images-fonts-and-files)
