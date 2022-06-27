# helper-functions

## Angular 

### convert Image to Base64
```ts
blobToBase64(blobData: Blob): Promise < Base64 > {
    return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onloadend = () => {
            const base64data = reader.result as Base64;
            resolve(base64data);
        };
        reader.onerror = () => {
            reject(new DOMException('Problem parsing input file.'));
        };
        reader.readAsDataURL(blobData);
    });
}

// expemple: assetImagePath = '/assets/images/cv-doc-header.png'; or http url
async imageToBase64(assetImagePath): Promise < Base64 > {
    return this.http.get(assetImagePath, { responseType: 'blob' }).pipe(
        map(async (blobData: Blob) => {
            return await this.blobToBase64(blobData);
        })
    ).toPromise();
}
```
