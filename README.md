# Mac + XAMPP 8+, missing intl issue


1. Go to "/Applications/XAMPP/htdocs/codeigniter4/system/CodeIgniter.php" -- line 208

Before:
$requiredExtensions = [
      'intl',
      'json',
      'mbstring',
];

After:
$requiredExtensions = [
      //'intl',
      'json',
      'mbstring',
];



2. Go to "/Applications/XAMPP/htdocs/codeigniter4/system/CodeIgniter.php" -- line 186

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



3. /Applications/XAMPP/htdocs/codeigniter4/system/I18n/Time.php -- line 78

Before:
-------------------------------------------------------------------------------------
$this->locale = $locale ?: Locale::getDefault();

After:
-------------------------------------------------------------------------------------
$this->locale = 
if(function_exists('locale_set_default')) {  
    $this->locale = $locale ?: Locale::getDefault();
}





