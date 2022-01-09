# Routing in Microfrontend

## Inflexible Requirement #1

### Both the Container + Individual SubApps need routing features

- Users can navigate around to different apps using routing logic built into the container.
- User can navigate around in a subapp using routing logic built into the subapp itself.
- Not all subapps will require routing.

#### Solution-1

The container and each subapp can optionally have a routing library.

## Inflexible Requirement #2

### Sub-apps might need to add in new pages/routes all the time

- New routes added to a subapp should require a redeploy of the container.

#### Solution-2

- Continer's routing will be used to decide which microfrontend to show.

### Inflexible Requirement #3

### We might need to show two or more microfrontends at the same time

- This will occur all the time if we have some kind of sidebar nav that is built as a separate microfrontend.

#### Solution-3

- Continer's routing will be used to decide which microfrontend to show.

### Inflexible Requirement #4

### We want to use off-the-shelf routing solutions

- Building a routing library can be hard - we don't want to author a new one!
- Some amount of custom coding is OK.

### Inflexible Requirement #5

### We need navigation features for sub-apps in both hosted mode and in isolation

- Developing for each environment should be easy - a developer should immediately be able to see what path they are visiting

### Inflexible Requirement #6

### If different apps need to communicate information about routing, it should be done in as generic a fashion as possible

- Each app might be using a completely different navigation framework.
- We might swap out or upgrade navigation libraries all the time - shouldn't require a rewrite of the rest of the app.

Routing libraries decide what content to show on the screen

History -> Object to get and set the current path the user is visiting.

Router -> Shows different content based on the current path.

Browser History -> Look at the path portion of the URL to figure out what the current path is.

Hash History -> Look at everything after the # in the URL to figure out the current path.

Memory or Abstract History -> Keep track of the current path in memory

Container - React Router using Browser History

Marketing - React Router using Memory history

Auth - React Router using memory history

- Use memory history routing in all children apps ( microfrontend )
- Use Browser history in container app

User clicks Link governed by container(Browser History).
Communicate change down to Marketing.
Marketing's Memory History should update its current path.

User clicks link governed by Marketing(Memory History).
Communicate change up to container.
Container's Browser History should update its current path.

### Communication through callbacks

            onNavigate
Container -------------> Marketing -----> Click on pricing link in the marketing app ---> Update memory history's current path to '/pricing'. Call onNavigate to tell container that the current path has been changed.
