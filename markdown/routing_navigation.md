# File-Based Routing

- Expo router uses file-based routing similar to Next.js.
- The file in 'app' folder is URL path.![[01.excalidraw]]
- Basic route: app/index.tsx
- If you want a new route, generate new file in app folder with .tsx.
- Add Link: `{ts icon} <Link></Link>` components in ==expo-router==

# Dynamic Routing

- If you want to make dynamic routing folder
  $\rightarrow$ Make folder or file name \[Something\]![[02.excalidraw]]
- When you extract id from file or folder

```ts title:'useLocalSearchParams'
import { useLocalSearchParams } from "expo-router";

export default function MovieDetailsScreen() {
  // Extract id parameter from app/movie/[id].tsx
  const { id } = useLocalSearchParams();
  // ...
}
```

# Group Routing

- Expo Router provides group routing, which allows you to <span style="background:rgba(160, 204, 246, 0.55)"><u>prevent a segment from showing in the URL</u></span> by using group syntax.![[01.excalidraw]]

## Code Explanation

### tabs

```tsx title:'_layout.tsx'
import { icons } from "@/constants/icons";
import { images } from "@/constants/images";
import { Tabs } from "expo-router";
import React from "react";
import { Image, ImageBackground, Text, View } from "react-native";
```

- import modules & components - \@: usually means <span style="background:#fff88f">root directory</span> of current project. - React: import react library
  > [!important]
  > the layout file name <span style="background:#fff88f">MUST BE</span> "\_layout.tsx"

```tsx title:'Tab icon'
const TabIcon = ({ focused, icon, title }: any) => {
  if (focused) {
    return (
      <ImageBackground
        source={images.highlight}
        className="flex flex-row w-full flex-1 min-w-[112px] min-h-16 mt-4 justify-center items-center rounded-full overflow-hidden"
      >
        <Image source={icon} tintColor="#151312" className="size-5"></Image>

        <Text className="text-secondary text-base font-semibold ml-2">
          {title}
        </Text>
      </ImageBackground>
    );
  }
  return (
    <View className="size-full justify-center items-center mt-4 rounded-full">
      <Image source={icon} tintColor="#A8B5DB" className="size-5"></Image>
    </View>
  );
};
```

- `{tsx icon}justyfy-center items-center`: align row, column center
- `{tsx icon}tintColor`: change icon color

```tsx title:'Tab'
const _layout = () => {
  return (
    <Tabs
      screenOptions={{
        tabBarShowLabel: false,
        tabBarItemStyle: {
          width: "100%",
          height: "100%",
          justifyContent: "center",
          alignItems: "center",
        },
        tabBarStyle: {
          backgroundColor: "#0f0D23",
          borderRadius: 50,
          marginHorizontal: 20,
          marginBottom: 36,
          height: 52,
          position: "absolute",
          overflow: "hidden",
          borderWidth: 1,
          borderColor: "#0f0D23",
        },
      }}
    >
      <Tabs.Screen
        name="index"
        options={{
          headerShown: false,
          title: "Home",
          tabBarIcon: ({ focused }) => (
            <TabIcon focused={focused} icon={icons.home} title="Home" />
          ),
        }}
      ></Tabs.Screen>

      <Tabs.Screen
        name="search"
        options={{
          headerShown: false,
          title: "Search",
          tabBarIcon: ({ focused }) => (
            <TabIcon focused={focused} icon={icons.search} title="Search" />
          ),
        }}
      ></Tabs.Screen>

      <Tabs.Screen
        name="saved"
        options={{
          headerShown: false,
          title: "Saved",
          tabBarIcon: ({ focused }) => (
            <TabIcon focused={focused} icon={icons.save} title="Saved" />
          ),
        }}
      ></Tabs.Screen>

      <Tabs.Screen
        name="profile"
        options={{
          headerShown: false,
          title: "Profile",
          tabBarIcon: ({ focused }) => (
            <TabIcon focused={focused} icon={icons.person} title="Profile" />
          ),
        }}
      ></Tabs.Screen>
    </Tabs>
  );
};
```

> [!important]
> **Why double{} at screenOptions?**
>
> > First {}: means this is for using JS in JSX
> > Second {}: menas object literal

#### Tabs.screen

- name: link file (e.g. name="saved" $\rightarrow$ saved.tsx)

### Index, profile, saved, search

![[03.excalidraw|800]]

> [!question]
> **What is the difference between `function`, `const = () => {}`?**
>
> > `function`: can hoisting (can call function before define function)
> > `() => {}`: cannot hoist(cannot call function before define function)
>
> **Why export from module ?**
>
> > For reusing codes
