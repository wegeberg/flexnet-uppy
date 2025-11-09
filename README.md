v. 2.0.0 - Nov 8th 2025

A custom version of Uppy with Dashboard and XHRUploader.

## Install
Download /dist/bundle.js and include it in your HTML
-- OR --
    # git clone https://github.com/wegeberg/flexnet-uppy.git
    # npm install
    # npm run build

## Use
    <script src="/flexnet-uppy/dist/bundle.js"></script>

    const uppy = new Uppy.Core({ 
        autoProceed: true,
        maxFileSize: 8000000
    });
    if (document.getElementById("drag-drop-area")) {
        // Optionally add meta fields
        uppy.setMeta({
            meta_1: meta_1,
            meta_2: meta_2,
        });
        uppy
            .use(Uppy.Dashboard, {
                target: '#drag-drop-area',
                inline: true,
                height: 200,
                locale: {
                    strings: { // Danish translation - add your own
                        dropPasteFiles: 'Slip billeder her, eller %{browse}',
                        browseFiles: ' Gennemse computer',
                        cancelUpload: 'Afbryd upload',
                    }
                }
            })
            .use(Uppy.XHRUpload, { 
                endpoint: '/path-to-upload-endpoint',
                fieldName: 'file'
            })
            .on('upload-success', (_, response) => {
                console.log(response);
            })
            .on('complete', () => uppy.clear());
    }
