`pptx` recipe generates office powerpoint presentations based on the uploaded pptx template  with [handlebars](/learn/handlebars) tags filled inside using Powerpoint application.

1. Open Powerpoint and create pptx file using handlebars templating engine.
2. Upload created pptx file as an asset to the jsreport studio
3. Create template, select pptx recipe and link the previously uploaded asset
4. Attach sample input data or scripts if needed
5. Run the template, you get back dynamically assembled pptx report

![pptx](/img/pptx.png)

## Examples

- [Basic](https://playground.jsreport.net/w/admin/Jix3rnoQ)

## Built-in helpers

### pptxSlides
Main helper used to multiply slides. The helper call should be placed on the slide and the system iterates over provided data and creates extra slide based on item's context.
```
{{pptxSlides item}}
 ```

[Example - Slides](https://playground.jsreport.net/w/admin/Jix3rnoQ)

### pptxList
Create a list with single item using Word and call the `pptxList` helper. It will iterate over provided data and create another list item for every entry.
```
 - {{#pptxList people}}{{name}}{{/pptxList }}
 ```

[Example - List](https://playground.jsreport.net/w/admin/QCStNYjG)

### pptxTable
Create a table with columns header and single row using Pptx. Call `{{#pptxTable}}` in the first cell of the data row and end the call `{{/pptxTable}}` at the last cell.

| columnA                       | columnB                 |
|-------------------------------|-------------------------|
| ---                           | ---                     |
| {{#pptxTable people}}{{name}} | {{email}}{{/pptxTable}} |

#### Vertical table
Use helper argument `vertical=true` for rendering vertical table

|       |                                             |   |
|-------|---------------------------------------------|---|
| name  | {{#pptxTable people vertical=true}}{{name}} |   |
| email | {{email}}{{/pptxTable}}                     |   |

### pptxImage

1. Prepare image placeholder using Powerpoint- place any image to the desired position and format it to your needs.
2. Insert to the slide a new text box with content `{{pptxImage src=myDataURIForImage}}`
3. Move the text box over previously created image
4. Select both image and text box and click group from the "Picture Tools/Format" toolbar
5. Run the template with `myDataURIForImage` prop in the input data and you should see the image replaced in the output.

[Example - Image](https://playground.jsreport.net/w/admin/MBHWcK~B)

`pptxImage` supports the following configuration properties:

- `src` (`string`) -> specifies the base64 dataURI string representation of the image to load or an url from which to fetch the image
- `usePlaceholderSize` (`boolean`) -> when true the dimensions of the image will be set to the same dimensions than the placeholder image defined on the pptx file. Ex: `{{pptxImage src=src usePlaceholderSize=true}}`
- `width` (`string`) -> specifies the width of the image, value can be in `px` or `cm`. when only `width` is set, the `height` will be automatically generated based on the aspect ratio of the image. Ex: `{{pptxImage src=src width="150px"}}`
- `height` (`string`) -> specifies the height of the image, value can be in `px` or `cm`. when only `height` is set, the `width` will be automatically generated based on the aspect ratio of the image. Ex: `{{pptxImage src=src height="100px"}}`

## Custom helpers
You can implement also your own custom helpers and use them in the word templates. The helpers section can be toggled in the studio using the "show helpers" button.

## Child templates
The recipe doesn't support using [child templates](/learn/child-templates) or [assets](/learn/assets) to insert another pptx file into one template. Both can be used just to insert text.


![office helpers](/learn/static-resources/office-helpers.png)

## Preview in studio
See general documentation for office preview in studio [here](/learn/office-preview).

## API

```js
{
  "template": {
    "recipe": "pptx",
    "engine": "handlebars",
    "pptx": {
       "templateAssetShortid": "xxxx"
    }
  },
  "data": {}
}
```


In case you don't have the office template stored as an asset you can send it directly in the API call.
```js
{
  "template": {
    "recipe": "pptx",
    "engine": "handlebars",
    "pptx": {
       "templateAsset": {
          "content": "base64 encoded word file",
          "encoding": "base64"
       }
    }
  },
  "data": {}
}
```
