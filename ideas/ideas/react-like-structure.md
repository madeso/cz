---
title: "React-Like Structure"
summary: "Ability to create a parent/child structure"
tags:
    - react
---


### References

### React
```ts
const Example = () => {
    return <div>Hello {this.props.toWhat}</div>;
}
```
is syntax sugar for
```ts
const Example = () => {
    return React.createElement("div", null, `Hello ${this.props.toWhat}`);
}
```
https://dev.to/dperrymorrow/using-react-without-jsx-no-build-14gg

### Dear Imgui
```cpp
if (ImGui::BeginMenuBar())
{
    if (ImGui::BeginMenu("File"))
    {
        if (ImGui::MenuItem("Open..", "Ctrl+O")) { /* Do stuff */ }
        if (ImGui::MenuItem("Save", "Ctrl+S"))   { /* Do stuff */ }
        if (ImGui::MenuItem("Close", "Ctrl+W"))  { my_tool_active = false; }
        ImGui::EndMenu();
    }
    ImGui::EndMenuBar();
}
```
This does not require any new features but matching Begin/End structures is only detected at runtime
https://github.com/ocornut/imgui/

### Jetpack compose
```kotlin
@Composable
fun ArtistCardArrangement(artist: Artist) {
    Row(
        verticalAlignment = Alignment.CenterVertically,
        horizontalArrangement = Arrangement.End
    ) {
        Image(bitmap = artist.image, contentDescription = "Artist image")
        Column { /*...*/ }
    }
}
```
https://developer.android.com/develop/ui/compose/layouts/basics
https://www.youtube.com/watch?v=6_wK_Ud8--0

Explanation: a body after a function call is just syntax sugar for passing that body as a last argument. I'm unsure how ui state is passed between functions.

### swift ui
```swift
struct AlbumDetail: View {
	var album: Album

	var body: some View {
		List(album.songs) { song in 
			HStack {
				Image(album.cover)
				VStack(alignment: .leading) {
					Text(song.title)
					Text(song.artist.name)
						.foregroundStyle(.secondary)
				}
			}
		}
	}
}
```
What does this even mean???