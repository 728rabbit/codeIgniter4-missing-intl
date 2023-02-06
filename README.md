# CodeIgniter4, Mac & XAMPP v8+, missing intl issue


Step1: Edit "/Applications/XAMPP/htdocs/codeigniter4/system/CodeIgniter.php" -- line 208

Before:
-------------------------------------------------------------------------------------
$requiredExtensions = [
      'intl',
      'json',
      'mbstring',
];

After:
-------------------------------------------------------------------------------------
$requiredExtensions = [
      //'intl',
      'json',
      'mbstring',
];


Step2: Edit "/Applications/XAMPP/htdocs/codeigniter4/system/CodeIgniter.php" -- line 186

Before:
-------------------------------------------------------------------------------------
// Set default locale on the server
Locale::setDefault($this->config->defaultLocale ?? 'en');

After:
-------------------------------------------------------------------------------------
// Set default locale on the server
if(function_exists('locale_set_default')) {  
    Locale::setDefault($this->config->defaultLocale ?? 'en');
}



Step3: Edit "/Applications/XAMPP/htdocs/codeigniter4/system/I18n/Time.php -- line 78

Before:
-------------------------------------------------------------------------------------
$this->locale = $locale ?: Locale::getDefault();

After:
-------------------------------------------------------------------------------------
$this->locale = 
if(function_exists('locale_set_default')) {  
    $this->locale = $locale ?: Locale::getDefault();
}





