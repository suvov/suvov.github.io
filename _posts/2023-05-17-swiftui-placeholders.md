---
layout: post
title: SwiftUI Placeholders
author: Vladimir Shutyuk
---

### Introduction
In modern iOS apps, it's common to have screens that load content from a server, which can take some time. When users open a screen that requires data loading, it's essential to provide feedback and communicate the loading process to them. While displaying a default loading spinner is a straightforward approach, there's an alternative method called Skeletons that is widely used in mobile and web applications. In this blog post, we'll explore how to use placeholders in SwiftUI to indicate loading states and enhance the user experience.

### SwiftUI's redacted modifier
Before SwiftUI and iOS 14 developers had to implement placeholders themselves or rely on third-party libraries. However, since iOS 14, SwiftUI provides a system API that makes it easier to create placeholders. By applying the `.redacted(reason: .placeholder)` modifier to a SwiftUI View, we can instantly turn it into a placeholder.

`Text("Hello world!").redacted(reason: .placeholder)`

*Hello World image*

### Implementing Placeholders in SwiftUI
To illustrate the usage of placeholders, let's consider an example of an app that displays a list of cities fetched from a server.

#### CityView
The CityView consists of a title, subtitle, and image. 

*City view image*

By adding the `.redacted(reason: .placeholder)` modifier to this view, we can visualize both the skeleton state and the actual content using SwiftUI's Preview feature.

*City view redacted image*

#### CityListView
The CityListView displays multiple cities as a scrollable list. 

*City list view image*

By applying the `.redacted(reason: .placeholder)` modifier to the view, it cascades down to the individual CityViews, creating a skeleton effect.

*City list view redacted image*

### Design Considerations
When deciding whether to show the actual view or its skeleton, one approach is to make the view's model optional. If the model is nil, the skeleton will be displayed; otherwise, the actual view will be shown. The placeholder model represents data that looks good as a skeleton.

`.redacted(reason: model == nil ? .placeholder : [])`

*City list view with skeleton and optional model*

#### CityListLoadingView
Alternatively, for more flexibility, we can create a separate view specifically for the loading state. In this case, we can use a CityListLoadingView that includes a placeholder model and apply the .redacted(reason: .placeholder) modifier to it.

*City list loading view*

### Managing States
Suppose we have a CitiesScreen that maintains a `CitiesScreenState`, which has two cases: `.loading` and `.loaded`. 

Depending on the current state, we can use either the CityListView or the CityListLoadingView. By separating the states, we ensure a clear distinction between the `.loading` and `.loaded` states. Additionally, it's possible to include an `.error` case and implement a dedicated CityListErrorView for loading error.

### Conclusion
Utilizing placeholders in SwiftUI allows us to effectively communicate the loading process to users, resulting in a better app experience. By leveraging the `.redacted(reason: .placeholder)` modifier and following good design practices, we can enhance the visual feedback during data loading. Feel free to download the [example project](https://github.com/suvov/SwiftUIPlaceholderExample) and explore how placeholders can be implemented in your own app.
