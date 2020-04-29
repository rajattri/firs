# Vehicle Switcher Feature

A customer may own multiple JLR Cars. <br>
The Vehicle Switcher Feature, which can be accessed in the `MORE`->`Switch Vehicle` section of the Remote App, allows a user to switch between their multiple cars.<br>
At the switch vehicle screen, display all vehicle's info(Nickname, Registration Number, VIN) that are registered to the users' account, with the active vehicle highlighted.<br>
Display the vehicles outline next to the info.<br>
Load status, subscriptions, and contact phone numbers for the newly switched active vehicle.<br>
Display an indication of progress while the vehicle is switched.<br>
If vehicle switch cannot be made, the active vehicle is unchanged.<br>
Active vehicle is persisted after restarting the application. 


## Important files in this feature

* `vehicle_switcher_item.xml`
		Consists of a background image, vehicle outline image, vehicle nickname text, registration number text, and VIN text. 
* `vehicle_switcher.xml`
		Consists of a toolbar, a progress frame, and a recycler view consisting of a list of vehicle_switcher_item. 
* `VehicleViewHolder.java`
		View Holder for Vehicle Switcher package, has one instance of vehicle_switcher_item.xml bound with it.
* `VehiclesAdapter.java`
		Contains list of attributes of all vehicles owned by the user, methods to publish VINs, set selected vehicles, show vehicles
* `VehicleSwitcherPresenter.java`
		Defines the View interface implemented by VehicleSwitcherActivity. Has methods to handle clicking on a vehicle, tracking events, errors.
* `VehicleSwitcherActivity.java`
		The only activity in the Vehicle Switcher package. Implements View interface defined in the presenter. Extends TrustedNetworkBaseActivity<View>.


## Vehicle View Holder

View Holder for Vehicle Switcher package, extends RecyclerView.ViewHolder. <br>
Uses ButterKnife to bind view with itself (the view holder). <br>
Each VehicleViewHolder has one instance of vehicle_switcher_item.xml bound with it.


Displays:
* The vehicles nickname
* The vehicles registration number
* Vehicle Identification Number
* Outlined icon of the vehicle
 

## Vehicles Adapter

Adapter for the Vehicle Switcher package, extends RecyclerView.Adapter<VehicleViewHolders> with one or more VehicleViewHolders attached to it. <br>
Manages vehicle_switcher frame.

Contains:
* List of attributes of all vehicles owned by the user
* Methods to publish VINs, set selected vehicles, show vehicles 


## Vehicle Switcher Presenter

Presenter for the VehicleSwitcher package. <br>
Extends TrustedNetworkBasePresenter<View>, which itself extends BasePresenter<View> <br>
Uses PerViewScope: Notifies dagger of the scope of the class.


Defines the View interface implemented by VehicleSwitcherActivity.


Methods to handle clicking on a particular vehicle, tracking events, handle errors. <br>


## Vehicle Switcher Activity

Implements View interface defined in the presenter. <br>
Extends TrustedNetworkBaseActivity<View> which itself extends BaseActivity<View>. <br>
Uses ButterKnife to bind to vehicle_switcher, which contains a toolbar and a RecyclerView.


* `Intent getStartIntent(final Context)` Used for navigation. When the *MORE* menu is expanded and you click on the item corresponding to VEHICLE_SWITCHER ClickEvent Enum object, this method is used to start this activity.  
* `boolean dispatchTouchEvent(final MotionEvent)` Delay in reporting touch event if so desired.
* `boolean onOptionsItemSelected(MenuItem)` Overridden from Activity class. Performs as intended for any MenuItem except home, otherwise closes the activity, and goes up a single level in the app UI.
* `void onInitialize() ` Sets up the RecyclerView and the ActionBar. VehicleSwitcherPresenter.onViewAttached() will be called next.
* `void onInject()` Build the Dagger Component and inject field dependencies of this Activity.
* `Observable<String> onVehicleClicked()` Calls the adapters onVehicleClicked() method to retrieve the vin of the vehicle that was clicked on.
* `void showVehicles(final List<VehicleAttributes>)`
* `void showSelectedVehicle(final String vin)`
* `void showProgress()`
* `void hideProgress()`
* `void showError(final JLRError)`


![](vehicleswitcher-uml.png)