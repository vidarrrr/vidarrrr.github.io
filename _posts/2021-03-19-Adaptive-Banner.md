---
layout: post
title: Adaptive Banner Implementation (My opinion)
---

Link to [Adaptive Banner](https://developers.google.com/admob/android/banner/adaptive)

I guess the main problem it is when first time is creating the framelayout will push the other components (down or up) and this could be some issues by admob => invalid traffic.

My solution is we should put in a layout this framelayout so there will be a fixed size space in app. But we should implement the size of layout so I preferred linearlayout (I used constrainlayout before but i couldn't be success if you know a better solution post it so when people need can check you blog).

**activity_main.xml** **Tabbed Activity Project**
		 <com.google.android.material.tabs.TabLayout
            android:id="@+id/tabs"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="?attr/colorPrimary" />
			
		<LinearLayout
            app:layout_constraintTop_toTopOf="parent"
            android:layout_width="match_parent"
            android:layout_height="80dp"
            android:id="@+id/linearLayout"
            android:layout_gravity="center"
            android:background="#000000"
            >

            <FrameLayout
                app:layout_constraintTop_toTopOf="parent"
                android:id="@+id/ad_view_container"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="5dp"
                />

        </LinearLayout>


**Activity.java**

	
	
	protected void onCreate(Bundle savedInstanceState) {
		...
		//implement adaptive banner from first link
		linearLayout=findViewById(R.id.linearLayout);
		...
	}
    private void loadBanner() {
        // Create an ad request. Check your logcat output for the hashed device ID
        // to get test ads on a physical device, e.g.,
        // "Use AdRequest.Builder.addTestDevice("ABCDE0123") to get test ads on this
        // device."
        /*AdRequest adRequest =
                new AdRequest.Builder().addTestDevice(AdRequest.DEVICE_ID_EMULATOR)
                        .build();*/
        AdRequest adRequest=new AdRequest.Builder().build();
        AdSize adSize = getAdSize();
        
        ViewGroup.LayoutParams layoutParams =linearLayout.getLayoutParams();
        layoutParams.height=adSize.getHeightInPixels(getApplicationContext())+30; 
        linearLayout.setLayoutParams(layoutParams);


        adView.setAdSize(adSize);


        // Step 5 - Start loading the ad in the background.
        adView.loadAd(adRequest);
    }
	
	
	
	
	