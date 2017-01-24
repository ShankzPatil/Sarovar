# Sarovar

<div ng-repeat="val in ['a','b','c']">
     <input
            type="radio"
            name="val"
            data-ng-model="role" 
            data-ng-value="val"
            ng-init="$index==0?(role=val):''"
      />
     {{val}}
 </div>
