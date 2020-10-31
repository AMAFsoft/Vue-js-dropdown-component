# Vue-js-dropdown-component
Vuejs dropdown component using Tailwind css

## Dependencies

- [Tailwind css](https://tailwindcss.com)
- [Unicon](https://github.com/antonreshetov/vue-unicons)
- proper.js

## How to

1. Installing proper.js

``npm i -E popper.js@1.15.0``

2. Copy dorpdown.vue file to your project folder

3. Example

```javascript

    <template>
        <div>
            <dropdown :text="'Actions'" :icon="'ellipsis-v'" :options="{}">
                <a href="#" 
                class="text-sm py-2 px-4 font-normal block w-full">
                Edit
                </a>
                <a href="#" 
                class="text-sm py-2 px-4 font-normal block w-full">
                Delete 
                </a>
            </dropdown>
        </div>
    </template>

    <script>
    import dropdown from "path_to_your_components/dropdown";

    export default {
        components:{dropdown}
    };
    </script>

```

Replace ``path_to_your_components`` with the where you put the *dropdown.vue* component file

## Options 
- textColor
    
    **Type** : String

    **Default** : "text-white"

- shadow
    
    **Type** : Boolean
    
    **Default** : true

- upperCase
    
    **Type** : Boolean
    
    **Default** : False

- backgroundColor
    
    **Type** : String
    
    **Default** : "bg-gray-800"

- iconClacces
    
    **Type** : String
    
    **Default** : *Empty string*


- iconW
    
    **Type** : Integer
    
    **Default** : 24

- iconH
    
    **Type** : Integer
    
    **Default** : 24


- hoverClasses
    
    **Type** : String
    
    **Default** : "hover:shadow-lg"


## Bonus

To close the dropdown by clicking everywhere else, add this javascript hack to your global js file : 

```javascript
window.addEventListener("click", function(e){
    let dropdowns = document.querySelectorAll('.dropdown.block');
    if (e.target.closest('.dropdown-wrapper')) {
        return false;
    }else{
        for (let i = 0; i < dropdowns.length; i++) {
            const d = dropdowns[i];
            d.classList.remove('block')
            d.classList.add('hidden')
        }
    }
})
```


