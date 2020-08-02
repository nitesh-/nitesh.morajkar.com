---
title: "How to select and share text with intents in android"
date: "2014-08-24"
slug: "how-to-select-and-share-text-with-intents-in-android"
description: 'This Android example explains how to select and share text via Intent. Very useful if you want to implement sharing feature in your app.'
image: '/images/blog/android-text-selection.jpg'
tags: ['android']
---

Selecting text from a textview and Sharing via Intents are two different things. There are many tutorials on the web, but very few of them explain to select and share text via Intents together. The objective of this tutorial is save time which we tend to waste for this simple task.<!-- more -->

Before we go ahead, lets lists down steps:

 1. Create a TextView.
 2. Register a custom text selection callback which overrides the default text selection callback.
 3. Add callback methods.
 4. Get the selected text from the TextView.
 5. Share the text via Intent.

Here we go:

In the MainActivity:

	public class MainActivity extends Activity {
		private TextView tv = null;
		
		@Override
		protected void onCreate(Bundle savedInstanceState) {
			super.onCreate(savedInstanceState);
			setContentView(R.layout.activity_main);
			
			tv = (TextView) findViewById(R.id.textview);
			
			// Register a callback when user selects text
			tv.setCustomSelectionActionModeCallback(new Callback() {
	
				@Override
				public boolean onActionItemClicked(ActionMode mode, MenuItem item) {
					switch(item.getItemId()){
						case R.id.menu_item_share:
							String selectedText = getSelectedText();
							shareIntent(selectedText);
							return true;
						default:
							break;
					}
					return false;
				}
	
				@Override
				public boolean onCreateActionMode(ActionMode mode, Menu menu) {
					// TODO Auto-generated method stub
					getMenuInflater().inflate(R.menu.share_menu, menu);
					return true;
				}
	
				@Override
				public void onDestroyActionMode(ActionMode arg0) {
					// TODO Auto-generated method stub
					
				}
	
				@Override
				public boolean onPrepareActionMode(ActionMode mode, Menu menu) {
					/**
					 * Use the following code if you want to remove the default icons (select all, cut or copy). 
					 */
					// Remove the "select all" option
		            //menu.removeItem(android.R.id.selectAll);
		            // Remove the "cut" option
		            //menu.removeItem(android.R.id.cut);
		            // Remove the "copy all" option
		            //menu.removeItem(android.R.id.copy);
					return false;
				}
				
			});
		}
		
		/**
		 * Returns the selected text
		 * @return String selectedText
		 */
		private String getSelectedText() {
			String selectedText = "";
			int min = 0;
	        int max = tv.getText().length();
	        if (tv.isFocused()) {
	            final int textStartIndex = tv.getSelectionStart();
	            final int textEndIndex = tv.getSelectionEnd();
	
	            min = Math.max(0, Math.min(textStartIndex, textEndIndex));
	            max = Math.max(0, Math.max(textStartIndex, textEndIndex));
	            selectedText = tv.getText().subSequence(min, max).toString().trim();
	        }
	        return selectedText;
	        // Perform your
		}
		
		/**
		 * Opens a share menu
		 * @param String selectedText
		 */
		private void shareIntent(String Text) {
			if(!Text.equals("")) {
				Intent shareIntent = new Intent(Intent.ACTION_SEND);
		        shareIntent.setType("text/plain");
		        shareIntent.putExtra(Intent.EXTRA_SUBJECT, "subject here");
		        shareIntent.putExtra(Intent.EXTRA_TEXT, Text);
		        startActivity(Intent.createChooser(shareIntent, "Share Via"));
			} else {
				Toast.makeText(this, R.string.empty_text, Toast.LENGTH_LONG).show();
			}
		}
	}

In the activity_main.xml:

    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    xmlns:tools="http://schemas.android.com/tools"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent"
	    android:paddingBottom="@dimen/activity_vertical_margin"
	    android:paddingLeft="@dimen/activity_horizontal_margin"
	    android:paddingRight="@dimen/activity_horizontal_margin"
	    android:paddingTop="@dimen/activity_vertical_margin"
	    tools:context="com.share.MainActivity" >

	    <TextView
	        android:id="@+id/textview"
	        android:layout_width="wrap_content"
	        android:layout_height="wrap_content"
	        android:text="@string/hello_world"
	        android:textIsSelectable="true" />
	
	</RelativeLayout>

Now create a menu xml share_menu.xml
		

    <?xml version="1.0" encoding="utf-8"?>
	<menu xmlns:android="http://schemas.android.com/apk/res/android" >
	    <item
            android:id="@+id/menu_item_share"
            android:showAsAction="always"
            android:title="Share"
            android:icon="@android:drawable/ic_menu_share" />
	</menu>

And we are done. I'm sure this should save a lot of your precious time. You can [download the code](https://db.tt/0GLPsOF2)

