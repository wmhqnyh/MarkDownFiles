### TabLayout在设置TabLayout.addTab(new Tab().)

    /**
       * The one-stop shop for setting up this {@link TabLayout} with a {@link ViewPager}.
       *
       * <p>This method will link the given ViewPager and this TabLayout together so that any
       * changes in one are automatically reflected in the other. This includes adapter changes,
       * scroll state changes, and clicks. The tabs displayed in this layout will be populated
       * from the ViewPager adapter's page titles.</p>
       *
       * <p>After this method is called, you will not need this method again unless you want
       * to change the linked ViewPager.</p>
       *
       * <p>If the given ViewPager is non-null, it needs to already have a
       * {@link PagerAdapter} set.</p>
       *
       * @param viewPager The ViewPager to link, or {@code null} to clear any previous link.
       */
      public void setupWithViewPager(@Nullable final ViewPager viewPager) {
          if (mViewPager != null && mPageChangeListener != null) {
              // If we've already been setup with a ViewPager, remove us from it
              mViewPager.removeOnPageChangeListener(mPageChangeListener);
          }

        if (viewPager != null) {
            final PagerAdapter adapter = viewPager.getAdapter();
            if (adapter == null) {
                throw new IllegalArgumentException("ViewPager does not have a PagerAdapter set");
            }

            mViewPager = viewPager;

            // Add our custom OnPageChangeListener to the ViewPager
            if (mPageChangeListener == null) {
                mPageChangeListener = new TabLayoutOnPageChangeListener(this);
            }
            mPageChangeListener.reset();
            viewPager.addOnPageChangeListener(mPageChangeListener);

            // Now we'll add a tab selected listener to set ViewPager's current item
            setOnTabSelectedListener(new ViewPagerOnTabSelectedListener(viewPager));

            // Now we'll populate ourselves from the pager adapter
            setPagerAdapter(adapter, true);
        } else {
            // We've been given a null ViewPager so we need to clear out the internal state,
            // listeners and observers
            mViewPager = null;
            setOnTabSelectedListener(null);
            setPagerAdapter(null, true);
        }
    }

---

    private void setPagerAdapter(@Nullable final PagerAdapter adapter, final boolean addObserver) {
            if (mPagerAdapter != null && mPagerAdapterObserver != null) {
                // If we already have a PagerAdapter, unregister our observer
                mPagerAdapter.unregisterDataSetObserver(mPagerAdapterObserver);
            }

            mPagerAdapter = adapter;

            if (addObserver && adapter != null) {
                // Register our observer on the new adapter
                if (mPagerAdapterObserver == null) {
                    mPagerAdapterObserver = new PagerAdapterObserver();
                }
                adapter.registerDataSetObserver(mPagerAdapterObserver);
            }

            // Finally make sure we reflect the new adapter
            populateFromPagerAdapter();
        }
    
---

    private void populateFromPagerAdapter() {
            removeAllTabs();

        if (mPagerAdapter != null) {
            final int adapterCount = mPagerAdapter.getCount();
            for (int i = 0; i < adapterCount; i++) {
                addTab(newTab().setText(mPagerAdapter.getPageTitle(i)), false);
            }

            // Make sure we reflect the currently set ViewPager item
            if (mViewPager != null && adapterCount > 0) {
                final int curItem = mViewPager.getCurrentItem();
                if (curItem != getSelectedTabPosition() && curItem < getTabCount()) {
                    selectTab(getTabAt(curItem));
                }
            }
        } else {
            removeAllTabs();
        }
    }
    
    
    不显示的问题在于 removeAllTabs()方法，修改设置tabLayout.setupWithViewPager(viewPager)，TabLayout绑定ViewPager  
    与addTab的执行顺序。
