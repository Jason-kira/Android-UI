## 可扩展的选择器 ##

使用：
main.xml 布局
<code>

	 <!-- 文字按钮 -->
  	<com.bob.component.ExpandableSelector
      android:id="@+id/es_sizes"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:layout_alignParentBottom="true"
      android:layout_alignParentLeft="true"
      android:layout_margin="@dimen/expandable_selector_margin"/>

  	<!-- 图片按钮 -->

  	<com.bob.component.ExpandableSelector
      android:id="@+id/es_icons"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:layout_alignParentBottom="true"
      android:layout_centerHorizontal="true"
      android:layout_margin="@dimen/expandable_selector_margin"
      android:background="@drawable/bg_expandable_selector_dark"
      expandable_selector:animation_duration="@integer/custom_animation_duration"/>

  	<!-- 自定义按钮样式 -->

  	<com.bob.component.ExpandableSelector
      android:id="@+id/es_colors"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:layout_alignParentBottom="true"
      android:layout_alignParentRight="true"
      android:layout_margin="@dimen/expandable_selector_margin"
      android:background="@drawable/bg_expandable_selector"
      expandable_selector:hide_background_if_collapsed="true"
      expandable_selector:hide_first_item_on_collapse="true">

    <Button
        android:id="@+id/bt_colors"
        android:text="@string/colors_expandable_selector_title"
        style="@style/ExpandableItemStyleHeader"/>

  	</com.bob.component.ExpandableSelector>


</code>

MainAcitivity.java

<code>

			/*
		 * Copyright (C) 2015 Karumi.
		 *
		 * Licensed under the Apache License, Version 2.0 (the "License");
		 * you may not use this file except in compliance with the License.
		 * You may obtain a copy of the License at
		 *
		 * http://www.apache.org/licenses/LICENSE-2.0
		 *
		 * Unless required by applicable law or agreed to in writing, software
		 * distributed under the License is distributed on an "AS IS" BASIS,
		 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
		 * See the License for the specific language governing permissions and
		 * limitations under the License.
		 */
		
		package com.bob.expandableselector;
		
		import android.os.Bundle;
		import android.support.v7.app.ActionBarActivity;
		import android.view.View;
		import android.widget.Toast;
		
		import com.bob.component.ExpandableItem;
		import com.bob.component.ExpandableSelector;
		import com.bob.component.ExpandableSelectorListener;
		import com.bob.component.OnExpandableItemClickListener;
		
		import java.util.ArrayList;
		import java.util.List;
		
		public class MainActivity extends ActionBarActivity {
		
		  private View colorsHeaderButton;
		  private ExpandableSelector colorsExpandableSelector;
		  private ExpandableSelector sizesExpandableSelector;
		  private ExpandableSelector iconsExpandableSelector;
		
		  @Override protected void onCreate(Bundle savedInstanceState) {
		    super.onCreate(savedInstanceState);
		    setContentView(R.layout.main_activity);
		    initializeColorsExpandableSelector();
		    initializeSizesExpandableSelector();
		    initializeIconsExpandableSelector();
		    initializeCloseAllButton();
		  }
		
		  //初始化自定义样式按钮
		  private void initializeColorsExpandableSelector() {
		    colorsExpandableSelector = (ExpandableSelector) findViewById(R.id.es_colors);
		    List<ExpandableItem> expandableItems = new ArrayList<ExpandableItem>();
		    expandableItems.add(new ExpandableItem(R.drawable.item_brown));
		    expandableItems.add(new ExpandableItem(R.drawable.item_green));
		    expandableItems.add(new ExpandableItem(R.drawable.item_orange));
		    expandableItems.add(new ExpandableItem(R.drawable.item_pink));
		    colorsExpandableSelector.showExpandableItems(expandableItems);
		    colorsHeaderButton = findViewById(R.id.bt_colors);
		    colorsHeaderButton.setOnClickListener(new View.OnClickListener() {
		      @Override public void onClick(View v) {
		        colorsHeaderButton.setVisibility(View.INVISIBLE);
		        colorsExpandableSelector.expand();
		      }
		    });
		    colorsExpandableSelector.setOnExpandableItemClickListener(new OnExpandableItemClickListener() {
		      @Override public void onExpandableItemClickListener(int index, View view) {
		        switch (index) {
		          case 0:
		            colorsHeaderButton.setBackgroundResource(R.drawable.item_brown);
		            break;
		          case 1:
		            colorsHeaderButton.setBackgroundResource(R.drawable.item_green);
		            break;
		          case 2:
		            colorsHeaderButton.setBackgroundResource(R.drawable.item_orange);
		            break;
		          default:
		            colorsHeaderButton.setBackgroundResource(R.drawable.item_pink);
		        }
		        colorsExpandableSelector.collapse();
		      }
		    });
		  }
		
		    //文字按钮
		  private void initializeSizesExpandableSelector() {
		    sizesExpandableSelector = (ExpandableSelector) findViewById(R.id.es_sizes);
		    List<ExpandableItem> expandableItems = new ArrayList<ExpandableItem>();
		    expandableItems.add(new ExpandableItem("XL"));
		    expandableItems.add(new ExpandableItem("L"));
		    expandableItems.add(new ExpandableItem("M"));
		    expandableItems.add(new ExpandableItem("S"));
		    sizesExpandableSelector.showExpandableItems(expandableItems);
		    sizesExpandableSelector.setOnExpandableItemClickListener(new OnExpandableItemClickListener() {
		      @Override public void onExpandableItemClickListener(int index, View view) {
		        switch (index) {
		          case 1:
		            ExpandableItem firstItem = sizesExpandableSelector.getExpandableItem(1);
		            swipeFirstItem(1, firstItem);
		            break;
		          case 2:
		            ExpandableItem secondItem = sizesExpandableSelector.getExpandableItem(2);
		            swipeFirstItem(2, secondItem);
		            break;
		          case 3:
		            ExpandableItem fourthItem = sizesExpandableSelector.getExpandableItem(3);
		            swipeFirstItem(3, fourthItem);
		            break;
		          default:
		        }
		        sizesExpandableSelector.collapse();
		      }
		
		      private void swipeFirstItem(int position, ExpandableItem clickedItem) {
		        ExpandableItem firstItem = sizesExpandableSelector.getExpandableItem(0);
		        sizesExpandableSelector.updateExpandableItem(0, clickedItem);
		        sizesExpandableSelector.updateExpandableItem(position, firstItem);
		      }
		    });
		  }
		
		    //初始化图片按钮
		  private void initializeIconsExpandableSelector() {
		    iconsExpandableSelector = (ExpandableSelector) findViewById(R.id.es_icons);
		    List<ExpandableItem> expandableItems = new ArrayList<ExpandableItem>();
		    ExpandableItem item = new ExpandableItem();
		    item.setResourceId(R.drawable.ic_keyboard_arrow_up_black);
		    expandableItems.add(item);
		    item = new ExpandableItem();
		    item.setResourceId(R.drawable.ic_gamepad_black);
		    expandableItems.add(item);
		    item = new ExpandableItem();
		    item.setResourceId(R.drawable.ic_device_hub_black);
		    expandableItems.add(item);
		    iconsExpandableSelector.showExpandableItems(expandableItems);
		    iconsExpandableSelector.setOnExpandableItemClickListener(new OnExpandableItemClickListener() {
		      @Override public void onExpandableItemClickListener(int index, View view) {
		        if (index == 0 && iconsExpandableSelector.isExpanded()) {
		          iconsExpandableSelector.collapse();
		          updateIconsFirstButtonResource(R.drawable.ic_keyboard_arrow_up_black);
		        }
		        switch (index) {
		          case 1:
		            showToast("Gamepad icon button clicked.");
		            break;
		          case 2:
		            showToast("Hub icon button clicked.");
		            break;
		          default:
		        }
		      }
		    });
		    iconsExpandableSelector.setExpandableSelectorListener(new ExpandableSelectorListener() {
		      @Override public void onCollapse() {
		
		      }
		
		      @Override public void onExpand() {
		        updateIconsFirstButtonResource(R.drawable.ic_keyboard_arrow_down_black);
		      }
		
		      @Override public void onCollapsed() {
		
		      }
		
		      @Override public void onExpanded() {
		
		      }
		    });
		  }
		
		  private void initializeCloseAllButton() {
		    final View closeButton = findViewById(R.id.bt_close);
		    closeButton.setOnClickListener(new View.OnClickListener() {
		      @Override public void onClick(View v) {
		        colorsExpandableSelector.collapse();
		        sizesExpandableSelector.collapse();
		        iconsExpandableSelector.collapse();
		        updateIconsFirstButtonResource(R.drawable.ic_keyboard_arrow_up_black);
		      }
		    });
		    colorsExpandableSelector.setExpandableSelectorListener(new ExpandableSelectorListener() {
		      @Override public void onCollapse() {
		
		      }
		
		      @Override public void onExpand() {
		
		      }
		
		      @Override public void onCollapsed() {
		        colorsHeaderButton.setVisibility(View.VISIBLE);
		      }
		
		      @Override public void onExpanded() {
		
		      }
		    });
		  }
		
		  private void updateIconsFirstButtonResource(int resourceId) {
		    ExpandableItem arrowUpExpandableItem = new ExpandableItem();
		    arrowUpExpandableItem.setResourceId(resourceId);
		    iconsExpandableSelector.updateExpandableItem(0, arrowUpExpandableItem);
		  }
		
		  private void showToast(String message) {
		    Toast.makeText(this, message, Toast.LENGTH_SHORT).show();
		  }
		}


</code>

效果图：
![效果图]("shili.png")