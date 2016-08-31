# elm-jsonp

Send HTTP requests to servers that implement strict CORS headers.

It emulates `elm-http`'s `Http.send` and `Http.get` API. POST requests have not
been implemented yet.

## Usage

Because we aren't allowed to publish packages with Native JS code, you'll either
have to clone this project into a `vendor/elm-jsonp` folder and add it to your
`elm-package.json` source-directories and alter the Native module name.

Or, you can use [`elm_self_publish`](https://github.com/NoRedInk/elm-ops-tooling/blob/master/elm_self_publish.py)
which will take care of changing the Native module to your project's user and name,
compiling the package, and copying it to your project's `elm-stuff/packages`. I'd recommend
using this script.

## Example

```elm
import Http
import Jsonp
import Json.Decode as Json exposing ((:=))
import Task exposing (Task)

type alias Info =
    { identified : Bool }
    
   
lookupInfo : Task Http.Error Info
lookupInfo =
    Jsonp.get infoDecoder ("https://api.twitch.tv/kraken")
    

infoDecoder : Json.Decoder Info
infodecoder =
    Json.object1 Info
        ("identified" := Json.bool)
```
