# Sarovar

http://blog.andreasgustafsson.se/javascript/angular-confirm-modal-angular-ui/

<!DOCTYPE html>
<html ng-app="confirm">
<head>
    <meta charset="UTF-8">
    <title>Angular Modal Confirm Directive</title>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" />
</head>
<body ng-controller="homectrl">
    <a ng-confirm-message="Close dialog and loose all changes?" ng-confirm="ok()">Close</a>
    <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/angularjs/1.4.5/angular.min.js"></script>
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/angular-ui-bootstrap/1.1.1/ui-bootstrap.min.js"></script>
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/angular-ui-bootstrap/1.1.1/ui-bootstrap-tpls.min.js"></script>
 
    <script type="text/javascript">
        (function () {
            'use strict';
 
            var app = angular.module('confirm', ['ui.bootstrap'])
            .controller('homectrl', ['$scope', function ($scope) {
                $scope.ok = function () {
                    alert('Ok click');
                }
            }]);
 
            app.directive('ngConfirm', ['$uibModal', function ($uibModal) {
                return {
                    restrict: 'A',
                    scope: {
                        ngConfirmMessage: '@',
                        ngConfirm: '&'
                    },
                    link: function (scope, element) {
                        element.bind('click', function () {
                            var modalInstance = $uibModal.open({
                                template: '<div class="modal-header"><h3 class="modal-title">{{confirmMessage}}</h3></div><div class="modal-footer"><button class="btn btn-primary" type="button" ng-click="ok()">OK</button><button class="btn btn-warning" type="button" ng-click="cancel()">Cancel</button></div>',
                                controller: 'ModalConfirmCtrl',
                                size: 'sm',
                                windowClass: 'confirm-window',
                                resolve: {
                                    confirmClick: function () {
                                        return scope.ngConfirm;
                                    },
                                    confirmMessge: function () {
                                        return scope.ngConfirmMessage;
                                    }
                                }
                            });
                        });
                    }
                }
            }])
                .controller('ModalConfirmCtrl', ['$scope', '$uibModalInstance', 'confirmClick', 'confirmMessge',
                    function ($scope, $uibModalInstance, confirmClick, confirmMessge) {
                        $scope.confirmMessage = confirmMessge;
                        function closeModal() {
                            $uibModalInstance.dismiss('cancel');
                        }
 
                        $scope.ok = function () {
                            confirmClick();
                            closeModal();
                        }
 
                        $scope.cancel = function () {
                            closeModal();
                        }
                    }]);
        })();
    </script>
</body>
</html>
