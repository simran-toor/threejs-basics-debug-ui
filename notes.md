# 10 DEBUG UI 
* essential aspect of any project is making debugging easy
* you must be able to change as many parameters as possible:
    * finding perfect colour
    * speed
    * quantity
    * etc. 
* allows to tweak on the go
* you can create your own debug UI using HTML/CSS/JS, there are already multiple libraries:
    - `dat.GUI`
    - `control-panel`
    - `ControlKit`
    - `Uil`
    - `Tweakpane`
    - `Guify`
    - `Oui` 
* the most popular one is `dat.GUI`
## EXAMPLE
* go to bruno-simon.com/#debug
* shows debug UI in action
## HOW TO IMPLEMENT DAT.GUI
* use `lil-gui` instead, `dat.gui` has vulnerabilities b/c not updated
    * `npm i --save lil-gui` 
* import 
    `import * as dat from 'lil-gui` 
* instantiate to add to site 
    `const gui = new dat.GUI()`
    * adds panel to top right but it's empty 
* different types of elements (tweaks) that can be added to panel:
    - `Range` - for numbers with min and max values
    - `Color` - for colours w/ various formats
    - `Text` - for simple texts
    - `Checkbox` - for booleans (true/false)
    - `Select` - for a choise from a list of values
    - `Button` - to trigger functions
    - `Folder` - to organise you panel if you have too many elements
## ADD ELEMENTS
* use `gui.add(...)` to add an element 
    - first param is an object
    - second param is the property you want to teak 
* to be able to move the mesh:
    - needs to be added after the concerned variable (after the mesh has been instantiated)
    ```
     gui.add(mesh.position, 'y')
     ```
* can only add `gui` on `objects` b/c you can change properties of that `object`
* set `min` value, `max` value, and `step` (or precision):
    ```
    gui.add(mesh.position, 'y', - 3, 3, 0.01)
    ```
* add other axis:
    ```
    // Debug
    gui.add(mesh.position, 'y', - 3, 3, 0.01)
    gui.add(mesh.position, 'x', - 3, 3, 0.01)
    gui.add(mesh.position, 'z', - 3, 3, 0.01)
    ```
* can also use the `min(...)`, `max(...)`, and `step(...)` method:
    ```
    gui
    .add(mesh.position, 'y')
    .min(-3)
    .max(3)
    .step(0.01)
    ```
* change the label with the `name(...)` method:
    ```
    .name('elevation')
    ```
    * better to have clear labels 
* Dat.GUI will change the type of tweak according to the type of property
* add a tweak for the `visible` property:
    ```
    gui
    .add(mesh, 'visible')
    ```
    * shows checkbox and did not have to specify that it's a boolean
* show wireframe:
    ```
    gui
    .add(material, 'wireframe')
    ```
    * can also access by `mesh.material` in this case not applicable b/c `material` is a property in this code
## COLORS
* need to use `addColor(...)` b/c GUI doesn't know it's not a simple string
    ```
    gui
    .addColor(material, 'color')
    ```
* use `onChange(...)` method to log when the tweak value changed 
    ```
    gui
    .addColor(material, 'color')
    .onChange( () => {
        console.log('colour changed')
    })
    ```
* use `material.color.set(...)` to upadate color 
    ```
       gui
        .addColor(material, 'color')
        .onChange( () => {
            material.color.set(material.color)
        })
    ```
## FUNCTIONS
* to trigger a function it needs to be stored in an `object`
* use `parameters` object to create a `spin` method:
    ```
    const parameters = {
        spin: () => {
            gsap.to(mesh.rotation, { duration: 1, y: mesh.rotation.y + Math.PI * 2 })
        }
    }
    ```

## HOW AND WHEN TO USE IT 
* You should add tweaks as you progress and not wait until the end of the projext 
