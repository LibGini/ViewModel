# ViewModel
Sharing data between two fragments using view model 


public class PageViewModel extends ViewModel {

    /**
     * Live Data Instance
     */
    private MutableLiveData<String> username = new MutableLiveData<>();

    public void setName(String name) {
        username.setValue(name);
    }

    public LiveData<String> getName() {
        return username;
    }
}

//inside fragment two
    @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        txtName = view.findViewById(R.id.textViewName);

        pageViewModel.getName().observe(requireActivity(), new Observer<String>() {
            @Override
            public void onChanged(@Nullable String s) {
                txtName.setText(s);
            }
        });
    }
    }
    
    //inside fragment one
      @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        TextInputEditText nameEditText = view.findViewById(R.id.textInputTextName);
           nameEditText.addTextChangedListener(new TextWatcher() {
               @Override
               public void beforeTextChanged(CharSequence s, int start, int count, int after) {

               }

               @Override
               public void onTextChanged(CharSequence s, int start, int before, int count) {
                   pageViewModel.setName(s.toString());
               }

               @Override
               public void afterTextChanged(Editable s) {

               }
           });

    }
    
