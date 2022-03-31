> Thinking

```
FragmentManager
FragmentTransaction
Fragment
    DialogFragment
```

> Memory

```
public class AskBrainFragment extends Fragment {
    @Override
    public void onAttach(@NonNull Context context) { }
    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) { }
    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) { return null; }
    @Override
    public void onActivityCreated(@Nullable Bundle savedInstanceState) { }
    @Override
    public void onStart() { }
    @Override
    public void onResume() { }
    @Override
    public void onPause() { }
    @Override
    public void onStop() { }
    @Override
    public void onDestroyView() { }
    @Override
    public void onDestroy() { }
    @Override
    public void onDetach() { }
    @Override
    public void onConfigurationChanged(@NonNull Configuration newConfig) { }
    @Override
    public void onLowMemory() { }
}

FragmentManager fragmentManager = getFragmentManager();
FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
fragmentTransaction.replace(R.id.content, new AskBrainFragment());
fragmentTransaction.add(new Fragment(), "");
fragmentTransaction.commit(); fragmentTransaction.commitAllowingStateLoss();
fragmentTransaction.commitNow(); fragmentTransaction.commitNowAllowingStateLoss();
fragmentManager.executePendingTransactions();

Fragment fragment = new Fragment();
fragment.setArguments(new Bundle());
fragment.getArguments();

class AskBrainFragment extends DialogFragment {
    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setStyle(DialogFragment.STYLE_NO_TITLE, R.style.UpdateAppDialog);
    }
}
```

