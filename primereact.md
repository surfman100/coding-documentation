## PrimeReact
An overview of the PrimeReact opensource components for React

a minimum to get going is:
```
import 'primereact/resources/themes/[sometheme]/theme.css';   //a theme
import 'primereact/resources/primereact.min.css';  //required: PrimeReact components
import 'primeicons/primeicons.css';  //required: Icons
import 'primeflex/primeflex.css';  //required: Grid
```

# Major Components
- **PrimeFlex** is a CSS utility library similar to Bootstrap or Tailwind. Just include the primeflex.css file
- **PrimeBlocks** are copy & paste UI blocks. Built on PrimeFlex

# Layouts
These consist of 3 main parts; 
- the application layout (App.js inside app folder is the html template for the base layout)
- layout resources (required resources for the layout are placed inside the *public/assets/layout* folder)
- theme resources for PrimeReact components (theme resources are inside *public/assets/theme* folder)
