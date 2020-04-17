# ViewModel
Sharing data between two fragments using view model 


     //on inside view model

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


     //inside fragment two onViewCreated
   
        txtName = view.findViewById(R.id.textViewName);

        pageViewModel.getName().observe(requireActivity(), new Observer<String>() {
            @Override
            public void onChanged(@Nullable String s) {
                txtName.setText(s);
            }
        });
    }
    }
    
    //inside fragment one onViewCreated
      
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
    
