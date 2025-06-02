Works with union types and get rid of some object in union type
```ts
// Union  
type AlbumState =  
  | {  
      type: 'released';  
      releaseDate: string;  
    }  
  | {  
      type: 'recording';  
      studio: string;  
    }  
  | {  
      type: 'mixing';  
      engineer: string;  
    };  
  
type NotRealesedAlbum = Exclude<AlbumState, { type: 'released' }>;  
  
// const notRealesedAlbum: NotRealesedAlbum = {  
//   type: 'released' ✅ Error - Good// }  
  
const notRealesedAlbum: NotRealesedAlbum = {  
  type: 'mixing',  
  engineer: 'test'  
}
```