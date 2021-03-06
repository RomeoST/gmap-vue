## Live example

<eg-base>
  <eg-polygon-simple />
</eg-base>

## Source code

```html
<body>
  <div id="root">
    <gmap-map :center="{lat: 1.38, lng: 103.8}" :zoom="12" style="width: 100%; height: 500px">
      <gmap-polygon :paths="paths" :editable="true" @paths_changed="updateEdited($event)">
      </gmap-polygon>
    </gmap-map>

    <ul v-if="edited" @click="edited = null">
      <li v-for="path in edited">
        <ol>
          <li v-for="point in path">
            {{point.lat}}, {{point.lng}}
          </li>
        </ol>
      </li>
    </ul>
  </div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.6.11/vue.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/gmap-vue@1.2.2/dist/gmap-vue.min.js"></script>

  <script>
    Vue.use(GmapVue, {
      load: {
        key: 'AIzaSyDf43lPdwlF98RCBsJOFNKOkoEjkwxb5Sc'
      },
    });

    document.addEventListener('DOMContentLoaded', function() {
      window.XXX = new Vue({
        el: '#root',
        data: {
          edited: null,
          paths: [
            [ {lat: 1.380, lng: 103.800}, {lat:1.380, lng: 103.810}, {lat: 1.390, lng: 103.810}, {lat: 1.390, lng: 103.800} ],
            [ {lat: 1.382, lng: 103.802}, {lat:1.382, lng: 103.808}, {lat: 1.388, lng: 103.808}, {lat: 1.388, lng: 103.802} ],
          ]
        },
        methods: {
          updateEdited(mvcArray) {
            let paths = [];
            for (let i=0; i<mvcArray.getLength(); i++) {
              let path = [];
              for (let j=0; j<mvcArray.getAt(i).getLength(); j++) {
                let point = mvcArray.getAt(i).getAt(j);
                path.push({lat: point.lat(), lng: point.lng()});
              }
              paths.push(path);
            }
            this.edited = paths;
          }
        }
      });
    });
  </script>
</body>
```
